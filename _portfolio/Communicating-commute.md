---
title: "Communicating my commute"
excerpt: "Insights gained from analyzing my Strava commuting data. Exporting my strava data into csv format, I use Pandas for data manipulation, and Matplotlib and Seaborn libraries for visualizations. Grouping the data into different subsets I gain insights into how my commute changed seasonally, what conditions were favourable and other trends."
classes: wide
header:
  image: assets/projects/Story_telling/daily2017.PNG
  teaser: assets/projects/Story_telling/daily2017.PNG
sidebar:
  - title: "Role"
    image: assets/images/bio-photo.jpg
    image_alt: "logo"
    text: "Data Storyteller"
  - title: "Responsibilities"
    text: "Extracting and relaying information gained from raw data"
gallery:
  - url: /assets/projects/Story_telling/weather.PNG
    image_path: assets/projects/Story_telling/weather.PNG
    alt: "count of weather conditions  during commute"
  - url: /assets/projects/Story_telling/temperature.PNG
    image_path: assets/projects/Story_telling/temperature.PNG
    alt: "morning and afternoon temperature"
  - url: /assets/projects/Story_telling/distance.PNG
    image_path: assets/projects/Story_telling/distance.PNG
    alt: "every ride distance"
  - url: /assets/projects/Story_telling/daily2017.PNG
    image_path: assets/projects/Story_telling/daily2017.PNG
    alt: "every ride in 2017"
  - url: /assets/projects/Story_telling/daily2018.PNG
    image_path: assets/projects/Story_telling/daily2018.PNG
    alt: "every ride in 2018"
---

I started cycling to work
- rehabilitate my knee damaged in an accident
- avoid sitting in traffic and
- get fit and healthy.

When I started cycling to work in 2014, my office was 6km away and I enjoyed (recently created) bicycle paths for most of the way. My office then moved to the CBD which increased my commute distance to just under 12km. By then I had been commuting to work (both office and sites all over the Southern Suburbs) for about 3 years. I started using [Strava](https://www.strava.com/athletes/18377851) to record my daily commute in December of 2016.

Quick note:
2017 would be my typical work commute for the year, the route I had taken for 2 years. In 2018 I studied At [EDSA](https://explore-datascience.net) which was about 8km from home. In 2019 I started a new job that was located in Tygerberg Office Park, 20km away from home. I have wanted to commute but unfortunately personal safety was a concern from both family and from speaking to experienced cyclists. <br>
The notebook can be found (here)[https://github.com/Wahe3bru/CommunicatingCommute]

{% include gallery caption="Here are some graphs from the EDA" %}

### Summary
I created a presentation of the insights, the slide deck which can be viewed [here](#)

#### Some Simple Stats

Category||2017|2018
-|-|-|-
Distance in km
|total distance|2853.82|1846.17
|average distance|10.77|8.47
|longest distance|24|12.1
|shortest distance|0|0.39
Temperature in *C
|temp range|
|highest temp|32.78|33.04
|lowest temp|6.12|3.24
|most common (rounded)|19|21.0
|most common weather condition|Clear|Clear
commute
|days commuted|147|114
|individual rides|265|218
|average time|0:31:42|0:26:04


### Insights
The biggest factor in me cycling that day was the weather, specifically rain. If it rained that morning I would have to take the car, if rain was ecpected the afternoon I would chance it. <br>
The second factor would be if the condition of my bike and my health. Typically if I had a puncture in the week most likely the next days commmute might be affected. If I was sick/injured I would take the car. I did xfit on Tuesday evenings, would that affect my commute?

There are 49 days where I travelled one way. Not in any month had I made complete return trips.
There are 7 trips that were incomplete, either due to weather or puncture.

comparing weekdays
- incomplete commutes
- - morning, no afternoon
- - incomplete morning, no afternoon
- - no morning, afternoon
- comparing 2017 vs 2018

 monthly average: ave hr, max hr, ave speed, max speed, weather_temperature, moving_time
for 2017 and 2018
