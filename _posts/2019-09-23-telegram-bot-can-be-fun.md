---
title: Telegram bot can be fun
last_modified_at: 2019-09-23T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Telegram
  - notes
  - thoughts
  - bot
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "I sometimes add a notification to the end of a long running script notifying me that it's done."
---

I have had Telegram for a very long time, unfortunately most people I know only use Whatsapp.
It's awesome to see all the new features the Telegram makes available, but it is unfortunate that I can share the excitement with a few. My friends went crazy with gifs and stickers in a Whatsapp msg. yay! /s

What I got most excited for was the availability of chatbots. I have many ideas but they are beyond my ability to implement (at this time). I do have a basic reporting bot that notifies me when a scraping job is completed, or if their was an error. I have a "wabo_home_bot" that tells me the current temperature and humidity in my home, as well as the outside temperature (from a weather api).

I plan to build some more basic bots for my home automation projects, and then have a home channel on telegram so everyone can view the notifications in a central place. Like the doorbell rang with a photo of the visitor, or a notification that the washing machine is done etc.

I sometimes add a notification to the end of a long running script notifying me that it's done.
The easiest way is to make an api call using `requests`. So made a lil function that I can pass a message to
and it gets sent via my notification bot.
```python
import requests

def bot_sendtext(bot_message):

    bot_token = 'bot_token_here'
    bot_chatID = 'my_chat_id'
    send_text = f'https://api.telegram.org/bot{bot_token}/  sendMessage?chat_id={bot_chatID}&parse_mode=Markdown&text={bot_message}'

    requests.post(send_text)
```
I mistakenly used `requests.post(send_text)` and that still worked :shrug:

I intended to send me a table with the seedling name, price and a picture of it. unfortunately, only a limited set of Markdown and html is supported. embedding picture/s is not one of them :( but if you send a link a preview is given at the end of the message.
So for each new seedling available, I send the name, with the price a markdown link to the picture of the seedling. like so:
```python
  bot_sendtext('There are new seedling/s available!')
  for i in range(len(new_name_li)):
      seedling_msg = f'{new_name_li[i]} [{new_price[i]}]({new_img_url[i]})'
      bot_sendtext(seedling_msg)
```
which results in:
![](/assets/images/seedling_notification.PNG)
The link is a link to the picture of the seedling, so if I click (touch) on the price or picture I view the entire picture. it also makes the price a different color, so the name and price are visually separated (not shown in this pic).
So abit of a hack but it serves it's purpose quite well.
