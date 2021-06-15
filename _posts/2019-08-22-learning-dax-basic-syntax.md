---
title: Learning DAX Basic syntax.md
last_modified_at: 2019-08-22T15:17:02-05:00
categories:
  - blog
tags:
  - PowerBI
  - notes
  - tutorial
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
---

In building reports using PowerBI I have started learning DAX.

I have very rudimentary excel skills, so this is all new to me.
Here's some basics on using DAX syntax:
```DAX
2 Months Ago Hours Billed =
VAR
    current_month=MONTH(TODAY())
RETURN
CALCULATE(
    ([HoursBilled] - [Regular Time Billed]),
    // Sum of Hours billed minus Regular Time billed
    FILTER('Query1', MONTH('Query1'[DateWorked])=current_month-2)
)
```
 - `2 Months Ago Hours Billed` - __descriptive names__ for the _measures_ as well as for _variables_. It helps in comprehension.
 - __spacing__ is important for readability. Personal preference has a lot to do with this, just keep it consistent.
 - VAR `current_month` gets todays (current) month, followed by a RETURN which leads to the formula*
 - `[HoursBilled]` and `[Regular Time Billed]` are measures previously created. Always use previously created measures as it improves readability (less cluttered code) and saves time.
 - `//` __comment__ your code when necessary. Here I explain the above measures.

*I think this means the variable created is only scoped within this measure.
