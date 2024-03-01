---
title: Long time, no see
date: 2024-02-14T21:03:32Z
draft: false
author: saugat
tags:
  - journey
  - updates
  - bots
  - blog
  - coding
  - research
summary: Been busy with everything so couldn't update here
---

Phew, that was a long gap on my blog. I just completed my 30-min run(3.4 Kms) 😅, which i will say is not much but 
is enough to make me feel a bit fresher. In summary, here are some of the things that happened in between:
### 🧑🏻‍⚕️ Physical health
I just started running (from today). I am currently jobless and eating junk while sometimes not even eating. I want to atleast make myself atleast a bit disciplined, as my dissertation is starting. My goal is set to burning 250kcal a day, while I burned twice that today.
{{< figure src="/fitness.jpeg" title="Apple fitness goal ring. 500Kcal for today 😮‍💨" >}}

### 🔬 My research
Completed my small 3000 words research before dissertation for my Uni and got score of 75. My title was "__​Comparative analysis of Artificial Bee Colony algorithm in solving data clustering problems__" (About which, I will update in my research page).

### 🤖 Bots and codes
I made few telegram bots in python as a refresher and personal itches. First one is [Music downloader](https://t.me/saugatgpt_bot), and other one I'm currently working on is [Musicer](https://t.me/SpotivnBot). I know, names are weird and both bots serve same purpose of searching and downloading music, both from different websites(ofc). The first one was made with python, initially was used for connecting to OpenAI api and getting answers directly, made with the purpose of using gpt4 just for myself cheap, but later I shifted to music downloader. I used [python-telegram-bot](https://pypi.org/project/python-telegram-bot/) on the first one, while the latter one is using javascript, leveraging [telegraf](https://telegraf.js.org). Here's the code (havent included the page that fetches api for searching). For now it just gives inline options for searching music. 
```javascript
const search : require('./helpers');

const bot : new Telegraf('my-token')

bot.start((ctx) => ctx.reply('Welcome'))
bot.help((ctx) => ctx.reply('Send me a sticker'))
bot.on(message('sticker'), (ctx) => ctx.reply('👍'))
bot.hears('hi', (ctx) => ctx.reply('Hey there'))
bot.on(message('text'), async (ctx) => {
  await ctx.reply(`Hello ${ctx.state.role}`)
})
bot.on('inline_query', async (ctx) => {
  const responses : await search(ctx.inlineQuery.query)
  return ctx.answerInlineQuery(responses)
})
```
⚠️  _Not to be viewed as an actual project_

### 🎓 Dissertation
With my dissertation going on, my topic is based on google play store reviews. I want to mine the reviews and try to make a model to find out painpoints in users for certain apps category. For example, if someone wants to know what issues are in currently existing music apps, or what features do user want in them, mining reviews is a great way of finding those out and include during development. So, as it is related to data analysis, I'm actually excited for this. __I will be posting about this in dissertation section of this page possibly every week with the updates.__

Well, that's about it for now but I am now blogging regularly, possibly every day or once every 2-3 days, including my dissertation updates. I might also start doing leetcode and other competitive programming, and update them accordingly.

 _**Sayonara**_ 👋🏼 and ***happy valentines day*** ❤️.