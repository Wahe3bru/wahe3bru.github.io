---
title: "Shell Scripting: Exit Status/Return Code"
date: 2018-09-05T15:34:30-04:00
categories:
  - blog
tags:
  - bash
header:
  overlay_image: https://source.unsplash.com/ieic5Tq8YMk/1280x900
---

These are useful with directional flow as well as for error checking.

### what are exit status / return code?
These are statuses returned after a script(or function) has run. <br>
`0` - when a script/function completed successfully
`1 - 255` - failed execution, where a number indicates the error. <br>
Exit statuses are usually used for error checking.
If no exit status is explicitly stated, then the status of the last executed command is used.

### $?
To check for the exit status of previously run code use `echo "$?"`<br>
`$/` can be used or assigned to a variable
examples:
```
# Using $?                            
HOST="google.com"                     
ping -c 1 $HOST                       
if [ "$?" -eq "0"]; then              
  echo "$HOST is reachable"           
else                                  
  echo "$HOST is unreachable"        
fi                                   
```
Assigning $? to a variable
```
HOST="google.com"
ping -c 1 $HOST
RETURN_CODE = $?
if "$RETURN_CODE" -ne "0";then
echo "$HOST is unreachable"
```
### exit command
- used to explicitly define the exit status
- the exit command stops the script
The command to defince the exit status is `exit {exit-code}`<br>
Rewriting the above example with exit codes:

```
# adding exit statuses                            
HOST="google.com"                     
ping -c 1 $HOST                       
if [ "$?" -eq "0"]; then              
  echo "$HOST is reachable"
  exit 0                               # no need to run rest of script            
else                                  
  echo "$HOST is unreachable"    
  exit 1                               # if error will exit script (return code 1)
fi
                                       # exit 0 is implicitly defined
```

The `exit 0` command could be put at the last line, but i think putting it on line 5 makes sense,
 as it will exit the script (and there is no need to run the rest of the script)

### return code for functions
Functions also return an 'exit status' upon completion returning a 0 (for success) or non-zero (between 1-255 for an error).
The same description applies to exit status of functions, the only difference is that the exit status is returned via the command `return {exit-code}`<br>
It makes sense that retrun command is used as the exit command will end the script.

more about functions in a later post.
