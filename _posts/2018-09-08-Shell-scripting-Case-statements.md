---
title: "Shell Scripting: Case Statements"
date: 2018-09-08T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

Case statements are used in place of multiple "if statements". To illustrate I will rewrite a previous example:
```
read -p "would you like to continue?" USER_RESPONSE
if $USER_RESPONSE -eq "yes"; then
  echo "then we shall"
elif $USER_RESPONSE -eq "no"; then
  echo "ok, see you soon"
  exit 0
else
  echo "sorry could you repeat that?"
fi
```
but first what is the syntax?
### CASE statement
case "$VAR" in
  pattern_1)           # pattern followed by ")"
    #commands-go-here  
    ;;                 # end pattern block with ";;"
  pattern_2)
    #commands-go-here
    ;;
esac                   # end case block

So lets rewrite the previous if statement:
```
read -p "would you like to continue?" USER_RESPONSE
case "$USER_RESPONSE" in
  [Yy]*)
    echo "then we shall"
    ;;
  [Nn]*)
    echo "ok, see you soon"
    ;;
  *)
  echo "sorry could you repeat that?"
esac
