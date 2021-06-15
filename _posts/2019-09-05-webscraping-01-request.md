---
title: Adventures in webscraping-01-requests
last_modified_at: 2019-09-05T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - webscraping
  - notes
  - tutorial
  - requests
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8574854/1024x720
excerpt: "To start this series of learning to webscrape, I figured it best to start at getting the data using `requests`"
---
To start this series of learning to webscrape, I figured it best to start at getting the data using `requests`.
Python does have a builtin library to do web requests but the `requests` library is super nice!<br>
__note:__ If given the choice it is always better to use the provided api. But sometimes their is no api, or the data you wish to obtain is not
available via the api. Then one would need to scrape the website. but always check for an api first.

so lets jump into it!<br>
The most common HTTP methods is GET.
The GET method indicates that you are trying to retrieve (ie get) data from the url.

saving the return value of the get() is an instance of `Response`, though not needed  it is typically
saved as response, res or r.
Your  `response` can give info about the results of the get() request.

##### Status codes
`response.status_code`

informs you about the status of the request, 200 OK means success whereas 404 NOT FOUND means resource was not found for more info on [status codes](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes) but basicaly:
- 1xx (Informational): The request was received, continuing process
- 2xx (Successful): The request was successfully received, understood and accepted
- 3xx (Redirection): Further action needs to be taken in order to complete the request
- 4xx (Client Error): The request contains bad syntax or cannot be fulfilled
- 5xx (Server Error): The server failed to fulfill an apparently valid request

##### The Content
`response.content` - gives you access to the raw bytes
`response.text` - returns a string (request guesses the encoding based on the response's headers)
`response.json()` - returns a dictionary so values in the object can be accessed by key

I will probably be best to explain params and headers via example.<br>
Using https://icanhazdadjoke.com/api

##### Query String Parameters
parameters are passed with the query as key-value pairs.<br>
This gets a dad joke with a fruit in it.
`https://icanhazdadjoke.com/search?term=fruit&limit=1`

In order to get a variable amount of jokes with the term we want it would be easier
to do it programmatically using `params` parameter.
```python
url = 'https://icanhazdadjoke.com/search'
number_of_jokes = 5
topic = 'dogs'

res = response.get(
      url,
      params={"limit": number_of_jokes, "term": topic}
)
```

##### Headers
To customize the header, pass in a dictionary of HTTP headers using the `header` parameter.
for example documentation for the api for [icanhazdadjoke.com](https://icanhazdadjoke.com/api)
adjusts the response formatting based on the provided HTTP `Accept` header
Accepted Accept headers:

- text/html - HTML response (default response format)
- application/json - JSON response
- text/plain - Plain text response

```python
res = requests.get(
    url
    params={"limit": number_of_jokes, "term": topic},
    headers={"Accept":"application/json"}
)
```
