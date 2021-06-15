---
title: Seedling data webscraper update
last_modified_at: 2019-09-20T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - webscraping
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8574854/1024x720
excerpt: "update replacing PhantomJS with the chromedriver"
---
 This is an update on my previous article on a [practical application]() of webscraping.
 I suggest you read that first to get up to speed.

 I realized when I ran the script that it would need to be updated as PhantomJS had been
 deprecated.
 The update replaces PhantomJS with the chromedriver, which supports running chrome headless.

 ```python
 # only new import
 from pathlib import Path

 chrome_driver_path = Path('C:/Users/WaheebA/Documents/work/learnings/webscraping/chromedriver.exe')

 chrome_options = webdriver.ChromeOptions()
chrome_options.headless = True
driver = webdriver.Chrome(executable_path=str(chrome_driver_path), options=chrome_options)
```
The driver now uses chromedriver, with the `executable_path` a string path to the executable (chromedriver.exe) and the added `option` being headless mode being True.

*The interesting thing to note is that the (pathlib) `Path` had to be converted to a string.

the above code replaces:
``` python
driver = webdriver.PhantomJS(executable_path='/Users/wahe3bru/Documents/phantomjs-2.1.1-macosx/bin/phantomjs')
```

The other minor changes to the script was removing the repetition by using `{}` in regex - the first number being the minimum matches and the optional second being the maximum matches.
```python
# extracting the first price
# before
seedling_df['price'] = seedling_df.price.apply(lambda s: re.findall(r'^(R\d{1,2}\.\d\d)',s)[0])
# after
seedling_df['price'] = seedling_df.price.apply(lambda s: re.findall(r'^(R\d{1,2}\.\d{2})',s)[0])

# getting rid of the uneccessary 'Seedling' and `\n` characters
# before
seedling_df['description'] = seedling_df.description.str.replace('\\n\\n','').str.replace('Seedling','')
# after
seedling_df['description'] = seedling_df.description.str.replace('\\n{1,2}','').str.replace('Seedling','')
```
