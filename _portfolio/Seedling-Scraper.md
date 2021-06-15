---
title: "Seedling Scraper"
excerpt: "Using Selenium to web scrape JavaScript driven website to extract data of available seedlings, store the data as well as available period in a database. Notifying me of new seedlings available using a telegram chatbot"
header:
  image: https://source.unsplash.com/AsRAyHIkOHk/1024x720
  teaser: https://source.unsplash.com/AsRAyHIkOHk/1024x720
sidebar:
  - title: "Role"
    image: "/assets/images/bio-photo.jpg"
    image_alt: "logo"
    text: "Organic Gardner, Hobbyist with no cape"
  - title: "Responsibilities"
    text: "Notifying of seedling variety updates and saving availability"
gallery:
  - url: /assets/images/seedlings.PNG
    image_path: assets/images/seedlings.PNG
    alt: "seedling information on website"
  - url: /assets/images/seedling_notification.PNG
    image_path: assets/images/seedling_notification.PNG
    alt: "seedling notification via telegram bot"
---

### Project Summary:
Using Selenium (in headless mode) I scrape the information available on the [Livingseed](https://livingseeds.co.za) website. The seedling info is saved in database, as well as the data it was available. If there are new seedlings available, the name, price and picture of seedling is sent via Telegram chatbot.

I am an avid organic gardener that would like to grow heirloom open pollinated vegetables. Livingseeds started selling seedlings, but due to their living nature, the seedlings are available in limited quantity and for a limited time. The seedlings on offer can change between 2-3 weeks with no set schedule. What is on offer is what is available.

The website is JavaScript driven and therefore scraping using BeautifulSoup is unsuccessful. I used Selenium that uses the Chrome webdriver to access the seedling webpage. I operate Selenium in headless mode as their is no need for the graphical interface of chrome browser. Initially I used PhantomJS but that is no longer recommended - it still worked for me but it is deprecated so I switched to the recommended usage of Chrome webdriver. The source data is parsed using BeautifulSoup to extract the relevant data.

I have a simple sqlite database with a seedlings tables that stores each seedlings information such as id, name, price, description and image url. And a second table that records the date of each seedling available.

If there are new seedlings (ie seedling data not previously stored in database), the new seedling information is sent to the telegram chatbot informing me of the new seedlings available as well as the name, price, description and image of the seedling.

{% include gallery caption="Here are images of the website and the notifications received" %}

This was a quick project I created to solidify my learning webscraping using BeautifulSoup and Requests libraries. My notes on [Requests](https://wahe3bru.github.io/blog/webscraping-01-request/) can be found [here as well](https://wahe3bru.github.io/blog/thoughts/requests-some-beautifulsoup/) as my notes on [BeautifulSoup](https://wahe3bru.github.io/blog/webscraping-02-beautifulsoup-tags/).
A blog posts explaining the script can be found [here](https://wahe3bru.github.io/blog/webscraping,practical-application/) - note at the time I was using PhantomJS.

__Note:__ This project is still in active development. I use projects to instill what I have learned and to experiment with new ideas. I am refactoring the code to put all helper functions in a separate script. I also plan to use Apache Airflow to schedule and run the webscraping and notification, which means refactoring the code adding email notification and other features. <br>
I am happy with the current Minimal Viable Product as it was relatively quick to implement whilst challenging, trying to extract data from a JavaScript driven website and adding notification via Telegram.
