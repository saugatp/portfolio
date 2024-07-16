---
title: IOS Day 15
date: 2024-07-16T01:14:00Z
draft: false
author: saugat
tags:
  - journal
  - logs
  - 100daysofios
  - animation
  - gap
keywords:
  - ios
summary: Animations in swiftUI is perfect
---

### Doing: Understood animation in swiftui
Today, I've pretty much understood the way views are animated in SwiftUI. It's a complex topic, however in SwiftUI is implemented so elegantly and easily, even a layman could code a complex animation within minutes. Everyday, iOS development doesnt fail to make me feel amazed. I've within a hour of viewing some tutorials from [this medium article](https://medium.com/@midhlag55/swiftui-animations-the-basics-of-animations-and-transitions-5dfae5ce4268), and [this video](https://developer.apple.com/videos/play/wwdc2023/10156/) from apple's own developer page, I was able to implement a draggable circle that has scaling and shadow animations within a few line of code. 

```Swift
import SwiftUI

struct SettingView: View {
    @State private var dragging = false
    @State private var position = CGSize.zero

    var body: some View {
        Circle()
            .fill(.blue)
            .shadow(radius: dragging ? 10 : 0)
            .frame(width: 100, height: 100)
            .scaleEffect(dragging ? 1.1 : 1.0)
            .animation(.smooth, value: position)
            .offset(x:position.width, y: position.height)
            .gesture(DragGesture().onChanged{
                value in
                position = value.translation
                if !dragging {
                    withAnimation{
                        dragging.toggle()
                    }
                }
            }.onEnded{
                value in
                withAnimation{
                    position = .zero
                    dragging = false
                }
            })
            
    }
}
```
The result of which can be seen here:
{{< youtube eF24J8ITXz4 >}}

### Addressing the gap
I was unable to continue my 100 days journey for 3 continuous days because I was sick for 2 days and one day I was gone for work. And it is really hard to follow a discipline until and unless life is sorted out and you have a fix job, which unfortunately I don't have right now. Still, I'm committed to my learning and challenge, as sickness is something that can hinder anyone's streak. Although I'm still left with headaches, I'm slowly recovering and learning things at a very slow rate. Which, I will improve with my conditions becoming better. That's all from my side.


Thank you for reading this.
And,
***Good night.***