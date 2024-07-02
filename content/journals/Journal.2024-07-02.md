---
title: IOS Day 5
date: 2024-07-02T01:14:00Z
draft: false
author: saugat
tags:
  - journal
  - logs
  - 100daysofios
keywords:
  - ios
summary: Day 5 of iOS development learning
---

### Day so far: Currently 4 PM
Had an interview at Lidl, as a customer assistant. It was good, however till date I've given multitude of such interviews, I'm beginning to not have any hopefulness. Will be doing the challenge later at arount 8PM.
I am hoping to update and publish my challenge in linkedin as well like I am doing in twitter. However, it feels like I will be publishing something I might not be able to finish. Till today I'm finding iOS development to be actually easy and more cohesive than Android. It's been a long time since I;ve done Kotlin and Java so there might be more changes, however I will also do some android programming when im free.

### Learning: Hacky way to load next pages
I pretty much understand the concept of viewmodels and dividing business logics as an app developer. However, I didn't want to learn about those at all, rather taking a hacky approach on adding load more button which calls the **observable model**(which also stores a counter) and a function which loads data as per the counter and appends them to the list. This approach works perfectly in learning situation and hack an app within hours. But, this is not a correct approach and it tangles a lot of UI logic and business logic. In theory, this can be scaled up to the purpose of adding a search functionality, also adding a function of getting details, calling different API, and pretty much a lot.

#### The code in question:

```Swift
@Observable
class ModalAppData{
    var appResults: [Result] = []
    var currentPage: Int = 1
    func loadData() async {
        let rslts = await loadUrl(page:currentPage)
        self.appResults.append(contentsOf:rslts)
        currentPage+=1
    }
    
    init() {
            Task {
                let rslts = await loadUrl(page:currentPage)
                self.appResults.append(contentsOf:rslts)
                currentPage+=1
            }
        }
}

func loadUrl(page:Int) async ->[Result] {
    
    guard let url = URL(string: "https://rickandmortyapi.com/api/character/?page=\(page)") else {
        print("Invalid URL")
        return []
    }
    do{
        let (data, _) = try await URLSession.shared.data(from: url)
        if let decodedResponse = try? JSONDecoder().decode(AppResult.self, from: data) {
            return decodedResponse.results
        }
    } catch{
        print("Error")
    }
    return []
}

```

#### And the UI logic

```Swift
NavigationSplitView{
            List(){
                Toggle(isOn: $favoritesOnly, label: {
                    Text("Show Alive Only")
                })
                ForEach(filteredLandmarks){ result in
                    HStack{
                        AsyncImage(url: URL(string: result.image)) { image in
                            image.resizable()
                        } placeholder: {
                            Color.green
                        }
                        .frame(width: 50, height: 50)
                        .clipShape(Circle())
                        VStack(alignment:.leading){
                            Text(result.name).lineLimit(1)
                            Text(result.status).font(.subheadline).foregroundStyle(.gray).lineLimit(1)
                        }
                    }
                }
                Button("Load More") {
                                Task {
                                    await modalAppData.loadData()
                                }
                            }
                
            }.animation(.default, value: filteredLandmarks)
                .navigationTitle("Rick and morties")
        } detail: {
            Text("Select a landmark")
        }
```

#### Working video
{{< youtube 1D4ZPPs2H3Q >}}

