---
title: IOS Day 6
date: 2024-07-03T01:14:00Z
draft: false
author: saugat
tags:
  - journal
  - logs
  - 100daysofios
keywords:
  - ios
summary: Day 6 {Expect chaos}
---

### Learning: Not much
Although my understanding of viewmodel was pretty much limited in the iOS domain, I tried to learn something new. However I couldn't find any reasonable tutorial or blogs in this sector. Maybe because I didn't search wide and long. But it seems like the use of ***ObservableObject*** is the way of going the viewmodel path in this sector. For this I made a todo API that only has functionality of getting and posting a single task. Then I added a ApiService class for those two calls: 
```Swift

class ApiServicee{
    func fetchTodos() async throws -> [TodoItem]{
        let url = URL(string: "https://saugat45.pythonanywhere.com/todos")!
                let (data, _) = try await URLSession.shared.data(from: url)
                let todos = try JSONDecoder().decode([TodoItem].self, from: data)
                return todos
    }
    func addTodo(_ todo: TodoItem) async throws {
            let url = URL(string: "https://saugat45.pythonanywhere.com/todos")!
            var request = URLRequest(url: url)
            request.httpMethod = "POST"
            request.setValue("application/json", forHTTPHeaderField: "Content-Type")
            let staticJson: [String: Any] = [
                "task": todo.task,
            ]
            let jsonData = try JSONSerialization.data(withJSONObject: staticJson, options: [])
            request.httpBody = jsonData
            
            let (_, response) = try await URLSession.shared.data(for: request)
            guard (response as? HTTPURLResponse)?.statusCode == 200 else {
                throw URLError(.badServerResponse)
            }
        }
}
```
However, even though I tried a lot of ways, I was always getting a random error of bad request in the post method. Currently too tired to debug, but I tried converting string to json and other similar techniques that I could find. Still not fixed. In term of the ***Viewmodel*** in question, here it is:

```Swift
import Foundation

@MainActor
class TodoViewModel: ObservableObject{
    @Published var todos: [TodoItem] = []
    @Published var isLoading = false
    @Published var errorMessage: String?
    
    private let apiService = ApiServicee()
    
    func fetchItems() async {
           isLoading = true
           do {
               todos = try await apiService.fetchTodos()
           } catch {
               errorMessage = "Failed to fetch items: \(error.localizedDescription)"
           }
           isLoading = false
       }
    
    func addItem(task: String) async {
            let newItem = TodoItem(task: task)
            do {
                try await apiService.addTodo(newItem)
                todos.append(newItem)
            } catch {
                errorMessage = "Failed to add item: \(error.localizedDescription)"
            }
        }
}
```

I mean, I still dont know what @MainActor means, but this code is pretty much an observable class with @Published variables meaning the items are prone to change. I learnt these from [this medium post](https://azamsharp.medium.com/building-large-scale-apps-with-swiftui-a-guide-to-modular-architecture-9c967be13001)
After that, I hacked together a simple UI for showing the fetched task and a dialog for adding new task getting some ideas scraped from this [very good website](https://peterfriese.github.io/MakeItSo/tutorials/makeitso/01-building-a-simple-todo-list-ui/) I found which I will be taking a look over in coming days.

Anyways, that's it. Here are some screenshots although not necessary.
{{< figure src="/tasks.jpeg" title="Home screen that fetched the tasks" >}}
{{< figure src="/addtask.jpeg" title="Unnessary screenshot of task add dialog" >}}

Thank you