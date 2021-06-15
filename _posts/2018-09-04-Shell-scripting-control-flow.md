---
title: "Shell Scripting: Control flow"
date: 2018-09-04T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

### test
This is a shell built in, but commonly called as `[ condition-to-test ]`.<br>
Therefore it needs to be surrounded by spaces. so `if [$name="waldo" ]` will be interpreted as _if test$name = "waldo ]_ <br> It returns a boolean (True if correct, otherwise False) that is used to control flow.

Some arithmatic  operators:<br>
`-eq` | = and `-ne` | != <br>
`-lt` | < and `-le` | <= <br>
`-gt` | > and `-ge` | >=

some useful file operators:<br>
`-d file_name` | true if file is in directory <br>
`-e file_name` | true if file exists <br>
`-z string`    | true if string is empty <br>
`-n string`    | true if string is not empty <br>

[insert example here]
1. check if file exists
1. check if file in directory

### if statement
```
if [ condition-to-test ]
then  
  _command/s to be done_
else
  _command/s to be done_
fi  # backwards 'if' to denote end of if statement
```
`then` needs to be on a separate line unless, like multiple statements on a single line, preceded by a semi-colon. Though not recommended, it is sometimes used for readability.

Multiple 'else if' statements can be used aswell
```
if [ condition-to-test ]; then  
  _command/s to be done_
elif [ 2nd-condition-to-test ]; then
  _command/s to be done_
elif [ another-condition-to-test ]; then
  _command/s to be done_
else
  _command/s to be done_
fi
```
### && and; or ||

using the following if statement as an example:
```
HOST="google.com"
if not $HOST; then
echo "$HOST is unreachable"
```
__&& (and) operator__ will execute the second command only if the first one is successful.<br>
a quick trick using and:

```
HOST="google.com"
ping -c 1 $HOST && echo "S{HOST} is unreachable"
```
In the above script, if google is unreachable (the 1st command is unsuccessful) then the second command runs.

__|| (or) operator__ will execute the second statement only if the 1st is unsuccessful.<br>
a similar trick using or:
```
HOST="google.com"
ping -c 1 SHOST || echo "S{HOST} is unreachable"
```
