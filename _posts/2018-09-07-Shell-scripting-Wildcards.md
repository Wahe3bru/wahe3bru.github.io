---
title: "Shell Scripting: Wildcards and User Input"
date: 2018-09-07T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

Wildcards are used for pattern matching. They are similar in many programming languages (like python), so this is just a summary of them.

### Read User Input (STDIN)
to read in user input, use the following command:<br>
`read -p "prompt" VAR`<br>
Where `"prompt"` is the test to be displayed, and the input from the user saved to `VAR`<br>

for example:<br>
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

### Wildcards
It's very similar to other regex so here's a quick summary.

wildcard | matches
---|---
* | zero or more chars
? | one char
\ | escaped char
[a,e,o] | specific chars
[!aci] | matches not including (exactly one char)
[:digit:] | only digits
[:alpha:] | only letters
[:alnum:] | alphanumeric
[:lower:] | only upper case letters
[:upper:] | only lower case letters
[:space:] | only white space (`\t`, `\n`, `\s`)

Some examples to illustrate:
