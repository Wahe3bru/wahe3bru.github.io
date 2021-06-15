---
title: Webscraping, practical application
last_modified_at: 2019-09-14T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - notes
  - thoughts
  - webscraping
  - BeautifulSoup
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8574854/1024x720
excerpt: "applying what I learned into something practical"
---

There's this [website]() that sells heirloom seeds as well as some selected seedlings. The seedlings available changes continuously and I thought this would be a perfect project to practice webscraping on.

my first attempt did not yield any results.
I was denied. To solve that I included a header that referred my request as coming from a firefox browser - success. but celebration came to early as I found the scraping returned None :(

I turns out that the website is dynamically generated using javascript. which means using `Requests` and `BeautifulSoup` was not gonna work in extracting the data.

I skipped to chapter 10 in webcraping with python and learned to use `Selenium` headlessly with `Phantomjs`. I had used Selenium before to scrape [South African Courtroom data]() and marvelled at the ghost in the machine automatically clicking on each listed court before clicking on to the next page.

Though I had heard of the term headless - without the browser actually opening and viewing the programmed actions, this was my first attempt at doing so.

Breaking the problem down into chunks makes it easier.<br>
The two objectives for this project were:
1. getting the items on the page
2. finding the next page link
3. parsing that page into a BeautifulSoup object
4. refactor and learn

So let's run through the script.
#### Running Headless aka _Ichabod Crane mode_
<div style="width:100%;height:0;padding-bottom:56%;position:relative;"><iframe src="https://giphy.com/embed/tI6qnVy9m8i9qlNoS2" width="100%" height="100%" style="position:absolute" frameBorder="0" class="giphy-embed" allowFullScreen></iframe></div><p><a href="https://giphy.com/gifs/nba-dance-tI6qnVy9m8i9qlNoS2">via GIPHY</a></p>

```python
from bs4 import BeautifulSoup
from selenium import webdriver

driver = webdriver.PhantomJS(executable_path='/Users/wahe3bru/Documents/phantomjs-2.1.1-macosx/bin/phantomjs')
driver.get('https://livingseeds.co.za/heirloom-seedlings')
```
Selenium uses PhantomJS - "a headless web browser scriptable with JavaScript." then gets the seedlings webpage.
Selenium has methods to get id's and other tags within the webpage but since I was learning `BeautifulSoup` I prefered to
parse the html using it
```python
# save the source (html structure) of the webpage
pageSource = driver.page_source
bs = BeautifulSoup(pageSource, 'html.parser')
```
#### Extracting the Data on the page
Once I have a BeautifulSoup object it is easy to capture the div that contains the relevant data <br>
`plant_list = bs.find_all('div', {'class': 'caption'})` returns a list of all the `div`'s with the `class='caption'`

![inspecting the page](/assets/images/page-inspect.png)

viewing the source it was easy to see that the name was in the first tag `h4`, the description was in the preceding `p` tag and the price was in the `p` with the `class=price`. nice. The plant image was a bit more tricky. I chose a way so that I could extract it within iterating through each plant in the plant_list.
```python
for plant in plant_list:
  name = plant.h4.get_text()
  description = plant.p.get_text()
  price = plant.find('p',{'class': 'price'}).get_text().strip()
  plant_pic = plant.parent.parent.find('div', {'class': 'image'}).find(src=True)['src']
```
lets break down how I got the image of the plant.<br>
`plant.parent` - refers to `<div>` one level above<br>
`.parent` - refers to `<div class="product-thumb">`<br>
`.find('div', {'class': 'image'})` refers to the `<div class="image">` highlighted in the pic<br>
`.find(src=True)['src']` finds the `src` attribute in the child `a` tag, which can be referenced like a dictionary by using the key `['src']`

#### Finding all the pages aka _I got next_.
Now that I knew how to get all the seedling data on the page I needed to scrape the data off all the seedling pages. Because of the variability of the seedlings I wouldn't know before hand how many pages there would be.

I noticed that there were four list elements (li) inside the `<div class="pagination">` and whatever page (number) I was on, that `li` would have the class `class="active"`. That meant that if there was another page available it would be the next link, hence:
```python
next_page = bs.find('li', {'class':'active'}).next_sibling
```
If there was another link I would get that page using `Selenium`'s `webdriver`, extract the source and parse it with `BeautifulSoup`

```python
if next_page:
  driver.get(next_page.find(href=True)['href'])
  pageSource = driver.page_source
  bs = BeautifulSoup(pageSource, 'html.parser')
```
I placed the code in a while (there's a next page) loop and created a DataFrame.

#### Cleaning the data
The data scraped was relatively clean. Even though I stripped the excess white space in price there were two prices (vat inclusive and ex vat) and there was extra white space between them. Every description started with 'seedling' and some had newline characters.

```python
seedling_df['price'] = seedling_df.price.apply(lambda s: re.findall(r'^(R\d{1,2}\.\d\d)',s)[0])
seedling_df['description'] = seedling_df.description.str.replace('\\n\\n','').str.replace('Seedling','')
```
I used regex to extract the first price and used string replace method to remove the unnecessary strings.

The full code can be found [on my github](https://github.com/Wahe3bru/seedling_scraper)

#### So what's next?
I'm thinking of creating a seedling availability catalogue using jinja templating and sending a weekly email. Or store the data in a database and use that data to create a small flask project. If I save the data daily I could maybe run some analysis - like when each seedling is available and rank them in availability. Have a telegram bot notify me if there are new seedlings or when a rare seedling is available.

I guess saving the data to a database allows more options. Allows for more automation as well.<br>
what this space...  
