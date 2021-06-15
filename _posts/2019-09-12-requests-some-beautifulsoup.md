---
title: Requests some BeautifulSoup
last_modified_at: 2019-09-12T15:17:02-05:00
categories:
  - blog
  - thoughts
tags:
  - python
  - BeautifulSoup
  - notes
  - tutorial
  - thoughts
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8574854/1024x720
excerpt:
---
In [webscraping with python, 2nd edition by Ryan Mitchell](http://www.pythonscraping.com/), the author uses the builtin
urllib library to get webpage
```python
from urllib.request import urlopen
from bs4 import BeautifulSoup

html = urlopen("http://www.pythonscraping.com/pages/warandpeace.html")
bs = BeautifulSoup(html.read(), 'html.parser')

nameList = bs.findAll('span', {'class':'green'}) for name in nameList:
    print(name.get_text())
```

in a [previous post]() I wrote about the [requests](https://2.python-requests.org/en/master/) module, so thought it would be helpful to show how the above example can be used with Requests
```python
import requests
from bs4 import BeautifulSoup

res = requests.get("http://www.pythonscraping.com/pages/warandpeace.html")
bs = BeautifulSoup(res.content)

nameList = bs.findAll('span', {'class':'green'}) for name in nameList:
    print(name.get_text())
```

The only difference being `requests.get(url)` saves the data to a requests object, that contains other data aswell as the webpage contents.
To make a BeautifulSoup object from the webpage, we parse the contents of the requests object via `res.content`
BeautifulSoup uses `html.parser` by default so it can be left out.

That's really all there is to parse webpages into BeautifulSoup objects to be able to scrape data. It is perfectly fine to use the builtin urllib library for this purpose, but I prefer to use requests as it allows further functionality.

An example would be to raise an exception if the url is inaccessible and stopping the script.
```python
res = requests.get("http://www.pythonscraping.com/pages/warandpeace.html")
if res.status_code != 200:
  raise Exception(f'There is a problem with the url. status code is: {res.status_code}')
bs = BeautifulSoup(res.content)
```
