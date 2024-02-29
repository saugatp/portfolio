---
title: Logging is hard
date: 2024-02-17T21:47:34Z
draft: false
author: saugat
tags: 
 - journal
 - notes
 - logs 
 - research
 - flutter 
 - firebase
---

For an overthinker like me, its all about .._thinking and ideas_ 💡. Whether it is good, bad or _ugly_, ideas are something i have learnt to generate within my __26 years of experience__. And I can call myself pretty skilled on that field as well. However, once in a blue moon, there are some really striking ideas that I want to write down or make a note of. But the problem is those ideas can strike any moment, like while sleeping, or trying to sleep, drinking coffee, listening to podcast, at the _toilet_ or while ___running___ 🏃. 

### ⚠ The problem 
The problem is not just ideas, but also logging in general. While I am logging things and ideas for myself as well as research, I need to add metadata such as __location, time, and (maybe mood..)__. There are plethora of note/journal taking apps, but each have certain limitations. Most important being syncing to the cloud. I have an Iphone, and android tablet, also an macbook, but i need something that syncs on all of them. One such thing is __google notes__, however it makes huge clutter of notes and cannot organise notes based on ideas and journalling on it is almost impossible 🤷. 

### 😟 What then?
I am thinking of making an app using __flutter__, that saves my journal on firebase and syncs automatically on all devices. Just for me, that's doable, but most important is the ___user interface___. My app should directly go to note writing page while I open it, making it easier to write something on the go, but when I'm done, it should save the location as well. Also included should be the image and mood options. Just including the moods on the bottom as optional and a button for attaching image if incase i need to. And everything should be done automatically on the background, including classifying and tagging the notes and journal, and automatically __generating a summary__ at the day end. 

### 💻 Technologies
Flutter, firebase or some alternative, and maybe some machine learning stuff for classifying my notes. I don't know how to do the last part. 

### 🕐 Starting when?
Probably starting tomorrow, as I can make the app and can do the syncing, my issue is classification. After i better understand how to implement classification, whether on-device or on the web(I'm thinking of firebase function that runs automatically at the end of every day). This app should be my logger for my research project(that's the aim for now at least). 

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logo=flutter&logoColor=white)

That's all for today, _goodnight_. 😴