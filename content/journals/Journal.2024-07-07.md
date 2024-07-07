---
title: IOS Day 9
date: 2024-07-07T01:14:00Z
draft: false
author: saugat
tags:
  - journal
  - logs
  - 100daysofios
keywords:
  - ios
summary: SwiftData and TFL Api
---

### Learning: Basic understanding of SwiftData and TFL api
I skipped yesterday for my day of learning ios development due to personal reasons. Although I had enough time to do so, I decided to skip for a reason. Anyways, continuing to my journey, today's lesson was about SwiftData and it's implementation in my TODO app. As well as I had some testing done with the TFL api and tried to understand the outputs and filter the required data for my app. 

#### SwiftData updates
Currently, I've only implemented local level SwiftData implementation using the same model for Todos as before, and implemented a delete function as well. I found it's implementation extremely easy and there are no boilerplate code needed. Just initiate a model with **@model**, create a container for those model databases and initiate them in the app initializer, and use them in UI views with the context from **@Environment(\.modelContext)**. That's it! No app database method is as easy to implement in my view. Although I've yet to implement this in a larger scale app(which definitely comes with implementation and migration headache), till now for the basics, I'm actually enjoying it. Certainly, apple has a better app development ecosystem than google.

##### Below is my model incase someone wants to see:
```Swift
import SwiftData

@Model
class TodoData{
    @Attribute(.unique) var id: String
    var isCompleted: Bool
    var task: String
    init(id: String = UUID().uuidString, isCompleted: Bool = false, task: String="") {
        self.id = id
        self.isCompleted = isCompleted
        self.task = task
    }
}
```

##### Whole app initialisation code:
```Swift
import SwiftData

@main
struct todosApp: App {
    let modelContainer: ModelContainer
    init() {
        do{
            modelContainer = try ModelContainer(for:TodoData.self)
        }
        catch{
            fatalError("Could not initialize ModelContainer: \(error)")
        }
    }
    var body: some Scene {
        WindowGroup {
            ContentView()
        }.modelContainer(modelContainer)
    }
}
```
##### And queried like this:
```SwiftUI
    @Query private var todos: [TodoData]
    @Environment(\.modelContext) private var context
```

#### TFL api update
For TFL api, I've understood the basics and have been testing the apis fetching <mark>Nearby Bus Stations</mark> based on geolocation and <mark>List of upcoming buses</mark> and been modifying the data required for my app which will be a simple app that will list the nearby bus station and will show the next buses for that station. That's about it, and the app will be as simple as possible, as I might/not add more options later. That's it for today, thank you for reading and,
***Good night.***