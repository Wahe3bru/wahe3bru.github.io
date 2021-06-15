---
title: "The learning Path and work meet"
last_modified_at: 2019-08-07T15:20:02-05:00
categories:
  - blog
tags:
  - python
  - Pandas
classes: wide
header:
  overlay_image: https://unsplash.com/photos/J3JMyXWQHXU/720X480
---

The key to learning new things is to quickly put what you've learned into practice.

I came across `pathlib` in research for a project that required me learning yaml. I realised
that pathlib was worth learning further and when a colleague asked for a small favour I gladly accepted.

request: "I need to 'anonymize' the numbers (for a dashboard he's building)" <br> only problem
is that there are 166 excel files that need the numbers 'anonymized'. <br> Luckily it is the last two columns of each excel file which means it is progrmatically possible :)

```python
# using pathlib
dir_xlsx = Path.cwd() / 'data'
xcells = list(dir_xlsx.glob('*.xlsx'))
```
using `Path` from `pathlib` I could easily set the path for the directory containing the .xlsx files.
then used the `.glob`method to search for all files with the .xlsx extension and get all the paths to the files in a list.

```python
def gen_numbers(num):
    if num == 0:
        return num
    return ((num*0.75) + float(str(abs(num*0.4//1))[::-1]))
```
This function is just me playing around :) <br> My colleague wanted the number different but  not too much different otherwise it would mess with his dashboard.

I was trying something with random.randrange() but I was not sure about the data in the columns. I had to work on 2 sample spreadsheets. The first one, both columns were all zero - hence I left the zero's in place.
The non zeros get replaced by 2/3 of original number plus the 2/5 of the number with the digits reversed. <br>
I realised that the `num*0.4//1` might seem strange but it was suppose to be random number between `num*0.2` and `num*0.4` but I was disturbed and only realised it now (o0ops ;) )

In my defense asking someone to do you a favour in the final hour of the work day before a (4 day) long weekend ... while my cpu was maxed out trying to encode features off of images to be used in facial recognition - was a bit irritating, but an interesting challenge and an exercise in using what I had just revised the day before.

The full code:
```python
import pandas as pd
import numpy as np
from pathlib import Path

def gen_numbers(num):
    if num == 0:
        return num
    return ((num*0.75) + float(str(abs(num*0.4//1))[::-1]))

dir_xlsx = Path.cwd() / 'data'
xcells = list(dir_xlsx.glob('*.xlsx'))

for sheet in xcells:
    df = pd.read_excel(sheet)
    df.iloc[:,-2:] = df.iloc[:,-2:].applymap(gen_numbers)
    df.to_excel(sheet, index=0)
```
It could use another iteration, delete unused numpy import, cleanup the function.<br>
I'm a bit pedantic like that. <br>I explained the code to an interested colleague, but the 'anonymized' numbers in the excel sheets were the actual result/value.

PS. I left on time
