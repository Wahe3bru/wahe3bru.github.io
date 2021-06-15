---
title: Scheduling scripts with cron
last_modified_at: 2019-10-09T15:17:02-05:00
categories:
  - blog
  - thoughts
tags:
  - python
  - Jupyter
  - notes
  - tutorial
  - thoughts
classes: wide
header:
  overlay_image: https://source.unsplash.com/collection/8375052/1024x720
excerpt: "Cron is a time-based job scheduler in Unix-like computer operating systems, its general-purpose nature makes it useful for things like downloading files from the Internet and downloading email at regular intervals"
---

I use raspberry pi's as power efficient computers to run scripts that does not require much processing power. To schedule a time to run the script I use cron. I am learning Apache Airflow and it also uses similar cron expression of five fields to schedule (explained quite eloquently in the picture below)
>The software utility cron is a time-based job scheduler in Unix-like computer operating systems. Users that set up and maintain software environments use cron to schedule jobs (commands or shell scripts) to run periodically at fixed times, dates, or intervals. It typically automates system maintenance or administration—though its general-purpose nature makes it useful for things like downloading files from the Internet and downloading email at regular intervals

>from  wikipedia

Cron is configured  by a simple text file, `crontab` - a configuration file that specifies shell commands to be run periodically.
The easiest way is to edit the crontab with the command `crontab -e`
each line represents a job and the syntax requires a cron expression of five fields followed by the shell command to be executed. The five fields represent the schedule and each field denoting: `minutes hour DayOfMonth Month DayOfWeek command`

![tree](/assets/images/cron.PNG)
_note:_ the * represents any.

here's some examples:
- to run command at 15 min past every hour `15 * * * *`
- to run command daily at 19:22 am `22 19 * * *`
- to run command daily at 6:59 pm `59 6 * * *`
- to run command at 5 am every Sunday `00 5 * * 0`
- alternative the command above `* 5 * * Sun`
- to run command 8:37 pm every 1st of the month `37 20 1 * *`
- to run command hourly on the 9th of September `0 * 09 09 *`

Here's a more complex one: */15 9-17 * * 1-3,5 log_my_activity.py <br>
*/15 - every fifteen minutes
9-17 - between office hours 9am to 5pm
* - every day of the month
* - every month of the year
1-3,5 - but only Mondays, Tuesdays, Wednessdays, and Fridays

There are also non-standard shorthand methods like:

Entry	|Description|	Equivalent to
-|-|-
@yearly (or @annually)	|Run once a year at midnight of 1 January	|0 0 1 1 *
@monthly	|Run once a month at midnight of the first day of the month	|0 0 1 * *
@weekly	|Run once a week at midnight on Sunday morning|	0 0 * * 0
@daily (or @midnight)|	Run once a day at midnight|	0 0 * * *
@hourly	|Run once an hour at the beginning of the hour|	0 * * * *
@reboot	|Run at startup|	N/A
