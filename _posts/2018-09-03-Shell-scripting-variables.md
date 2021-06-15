---
title: "Shell Scripting: variables and comments"
date: 2018-09-03T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

In order to be more proficient I decided to learn some basic shell scripting. In learning [versioning, using Git](#) I learned some basic [command line/terminal](#) and discovered the efficiency and utility in using terminal/command line. This, combined with raspberry pi tinkering led to me exploring shell scripting.<br>
Welcome to the first post on Shell Scripting.

### #!
The first line of a script usually has a shebang (`#!`) followed by the path to the program that should execute the script to follow. If no shebang then the default shell is used (depending on the system), but it is best practice to explicitly state the program/shell<br>
eg. `#! /bin/bash`
### Comments
Everything after a `#` will be ignored by the shell. Comments are for humans to read. Usually comments are for explanations for reasons or to provide other information.
### Variables
- variables have no spaces in the name
- variables are case sensitive, by convention ALL_CAPS
- only letters, numbers and underscores are allowed
- variables cannot start with a number
- when initiating a value to variable there must be no spaces between the equal sign, variable and value `VAR_NAME="value"`

Commands can also be saved to variables: `VAR_NAME=$(command)`

```
#! /bin/bash

MY_SPORT="run"

# echo "I used to $MY_SPORT" would also work, but i prefer the following.
echo "I used to ${MY_SPORT}"
```


Variables are accessed by `$VAR_NAME` or `${VAR_NAME}`.<br>
If I used `echo "I used to $MY_SPORT"` would print the same result.

Curly braces are used when directly preceding/following strings `echo "I use ${MY_SPORT}ing to keep fit"` would return "I use runing to keep fit". <br>
In contrast `echo "I use $MY_SPORTing to keep fit"` would return "I use to keep fit" as the shell would interpret `$MY_SPORTing` as a variable (with no value).
