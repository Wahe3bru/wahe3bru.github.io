---
title: Timestamp to Datetime
last_modified_at: 2019-09-11T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
---

I needed to extract a full years data from a table, but the date and time was encoded as Unix timestamp - the number of seconds between a particular date and epoch (January 1, 1970) at UTC.
So I needed to convert the first and last day of last year to timestamp.

I found the answer on stackoverflow
```python
from datetime import datetime
import time

time.mktime(datetime.strptime('2018-01-01 00:00:01', "%Y-%m-%d %H:%M:%S").timetuple())
```
which returns `1514757601.0` <br>

<br>

#### So let's understand what's happening

I needed the first date and time -> 2018-01-01 00:00:01
<br>

###### datetime.strptime()
`datetime.strptime('2018-01-01 00:00:01', "%Y-%m-%d %H:%M:%S")` converts the string of the date and time to a __datetime object__ `datetime.datetime(2018, 12, 31, 23, 59, 58)`

<br>

###### timetuple()?
`.timetuple()` is a method of a datetime.date instance, which returns an object of type time.struct_time.
a struct_time is a named tuple which has attributes representing both date and time fields, with a flag to indicate if Daylight Savings Time is active. best explained with an example:
```python
from datetime import date
todaysDate = date.today()
timeTuple = todaysDate.timetuple()
print(timeTuple)
```
returns<br>
`time.struct_time(tm_year=2019, tm_mon=9, tm_mday=11, tm_hour=0, tm_min=0, tm_sec=0, tm_wday=2, tm_yday=254, tm_isdst=-1)`<br>
named tuple means the year can be accessed `print(timeTuple.tm_year)`<br>
returns `2019`<br>
or month by using indices `print(timeTuple[1])`<br>
which returns `9`

<br>

###### time.mktime()
time.mktime() is a function that takes struct_time as an argument and returns the seconds passed since epoch in local time.

So the steps are:
- `datetime.strptime` converts the date and time to a datetime object
  `datetime.datetime(2018, 12, 31, 23, 59, 58)`
- `timetuple()` converts the datetime object to a struct_time
  `time.struct_time(tm_year=2018, tm_mon=12, tm_mday=31, tm_hour=23, tm_min=59, tm_sec=58, tm_wday=0, tm_yday=365, tm_isdst=-1)`
- `time.mktime()` then converts the struct_time to a timestamp which is seconds since epoch (result is actually of type float)
  `1546293598.0`

<br>

Now that I understand the code, I realised that it could be made shorter and easier to understand.
All we need is `time.mktime()` which requires a struct_time to return a timestamp.<br>
The `time.strptime()` function parses a string representing time and returns struct_time. <br>
So the code could be simplified to:
```python
import time

time.mktime(time.strptime('2018-12-31 23:59:58', "%Y-%m-%d %H:%M:%S"))
```
We don't require the datetime import, and it is much easier to understand.

Sometimes I use stackoverflow to get the solution to a problem if it's a once off.<br>
But if the solution is novel and/or most likely to be used again - I prefer to understand it. This time trying to understand the solution led me figuring out an easier solution. <br>
I had never explored the [`time` module](https://www.programiz.com/python-programming/time#introduction) before so am happy to know more about it now.
