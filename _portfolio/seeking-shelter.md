---
title: "Webscraping; information gathering for public benefit"
excerpt: "my first contribution to open source project"
header:
  image: /assets/images/seeking_shelter.png
  teaser: assets/images/seeking_shelter.png
sidebar:
  - title: "Role"
    image: "/assets/images/bio-photo.jpg"
    image_alt: "logo"
    text: "Data gathering"
  - title: "Responsibilities"
    text: "scrape and clean all available data on clinics and courts nation wide"
gallery:
  - url: /assets/images/seeking_shelter.png
    image_path: assets/images/seeking_shelter.png
    alt: "map of relevant institutions"
  - url: /assets/images/unsplash-gallery-image-2.jpg
    image_path: assets/images/unsplash-gallery-image-2-th.jpg
    alt: "placeholder image 2"
  - url: /assets/images/unsplash-gallery-image-3.jpg
    image_path: assets/images/unsplash-gallery-image-3-th.jpg
    alt: "placeholder image 3"
---

background<br>
For Madiba day [Codebridge]() held a "hack for social good" day, whereby institutions or individuals could describe their problems or project and hackers (of every kind) could team up and assist. I joined the team offering my data wrangling/cleaning skills but there was not much data to start with.<br>
{Project goals go here}<br>
I was super impressed by the guy next me who was a Ruby programmer. He learned to scrape the South African Police Service website to obtain the name and geolocation of each police station in South Africa. I was super motivated that he learned to do that in one day! Ruby is similar to python so figured that if webscraping was on my list of skills to learn, so why not bump it up the list - for a good cause. Having a goal always makes learning something new more interesting and worthwhile.
It took me a Sunday night to get the basics down so I could scrape all the clinic data from the South African Social welfare site.

{% include gallery caption="This is a sample gallery to go along with this case study." %}

__scraping clinic data__<br>
I used Requests and BeautifulSoup libraries in a Jupyter Notebook.
The website was easy to navigate and I extracted the url for each province manually.
After figuring out how to extract the wanted information from Eastern Cape, I generalised the script so that I could the data for the rest of the provinces.

It was not a very hard task, <explain>

__scraping the court room data__<br>
The official website offers a pdf of all the information of the various courts across South Africa.
Unfortunately the quality of the pdf was not good and the presentation of the data made it harder to extract relevant information.<br>
After struggling to extract data from four different pdf extraction tools I decided that it was best to extract the data from the official website. Only problem was that this website used Ajax/Javascript for it's layout. This meant that the structure of the webpage changed based on what the mouse clicked on. I could not use BeautifulSoup to extract the all the data at once like I did with the clinics but rather had automate manually clicking each court listed on the webpage, and then extracting the relevant information.

I used Selenium and targeted the relevant links (court names) and extracted the information displayed for the selected court.
I saved the data in a Pandas DataFrame and exported it as csv.
The scraped data had to be cleaned and I used Pandas string methods and some regex.
