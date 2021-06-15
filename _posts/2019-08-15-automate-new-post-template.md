---
title: automate new post template
last_modified_at: 2019-08-15T15:17:02-05:00
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
The whole reason for going static website generation was for the ease.
I have thoughts that run around in my head all day but i struggle to put them down.
It's like psyching yourself up to confront someone when you know your are in the right,
and then the moment comes...and goes... and you rationalize to yourself that it really wasn't such a big
deal anyway.

So I start writing my thoughts down and ramble on hoping to get to point. but the amount of activation energy
required often leaves me to abandon the ramble - _there is no point_

I started realizing that as I learn things I start connecting threads that maybe shouldn't be connected,
but writing them down definitely helps in retaining the knowledge.<br>
This blog was created to share some of my learnings and with the reboot I added a random thoughts section.<br>
The goal being that with enough practice I would get better at putting down my thoughts, organising and explaining
them.

To make it even easier I have created a script to create a template for a blog post.
all I need to do is think of a title and run the script like below
![python new_post.py](/assets/images/new_post.png)

iteration 1 of the new_post.py:
```Python
#!/usr/bin/Python
from datetime import datetime
from pathlib import Path
import sys

title = sys.argv[1]
date_string = datetime.now().strftime("%Y-%m-%d")
filename = date_string + "-" + "-".join(title.lower().split(" ")) + ".md"
path_file = Path() / '_posts' / filename

path_file.touch()
path_file.write_text(f'''---
title: {title}
last_modified_at: {date_string}T15:17:02-05:00
categories:
  - blog
tags:
  - python
  - Jupyter
  - notes
  - tutorial
---
''')
```
I am really liking the pathlib library, I can create a path to the "new_post" and create the file with `.touch()` - a new thing I learned :)<br>
and using the `.write_text` I can write to the file without worrying about opening and closing the file.

I have a jupyter notebook of notes and examples I took learning `Pathlib` which I will prolly post shortly.
