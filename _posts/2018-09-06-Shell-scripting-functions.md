---
title: "Shell Scripting: Functions"
date: 2018-09-06T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

Functions are just mini scripts that can be executed within a script. Therefore, a function can call another function provided that they are defined before execution.

### Functions
- reusable code
- must be defined before usage
- has parameter support

### What is parameter support?
Parameters given to a function can be accessed via $1 to $9 <br>
$0 is reserved for the script. for more examples check out the [repo](htttp://www.github.com/wahe3bru/shell_scripting).

```
#! /bin/bash

echo "my favourite colour is $1"
```
calling script: `fave_colour.sh blue`

### Creating a function
```
function function name(){
  # commands-go-here
}
```
```
function name2(){
  # commands-go-here
}
```

### Calling a function
Is as simple as calling the functions name, without parenthesis like most other languages eg

```
function fave_color(){
  echo "my favourite colour is Blue"
}
fave_color
```
### Variable scope
Variables are global by default, but it is best practice to make variables inside functions local. This is by using the keyword local<br> eg.`local VAR_NAME`
