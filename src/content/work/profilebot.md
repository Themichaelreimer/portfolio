---
title: Profile Bot
publishDate: 2022-05-14 00:00:00
img: /assets/projects/profilebot/dramatization.gif
img_alt: A simulation of what happens to my github profile over the year
description: |
  This bot rotates my github profile picture by (slightly) less than a degree a day, so that it rotates one full time per year
tags:
  - Python
  - Selenium
  - Botting
  - Cron
---

### August 1st - the one day per year where my profile looks normal

![](/assets/projects/profilebot/profilebot2.png)
### How it looks on any other day

### How it works:

The process is pretty simple:
- Each day, a cron job on a linux machine I own, is triggered that generates a new profile.png via a small python script. It takes a source image, and calculates the day's rotation using the date, and saves the output.
- A selenium script activates to log into my github account (via a .secrets file stored only on the machine running the script), and proceeds through the change profile picture dialog.
- Rinse and repeat

### Notes:
- Some GitHub organizations require 2FA on accounts. This bot can be extended to use a Twilio free trial account to handle 2FA. If this Twilio account sees low usage, then the free credits should last about a year
- In most cases, Selenium or similar tools are overkill. The Python requests library - with a little work - handles CSRF just fine. Unless proven otherwise, the best approach for botting is to figure out the site's web API by paying attention to how requests are being made, and to make them using straight HTTP requests. This will be faster for the developer, faster for the machine, and more resilient over time. In this case, I used Selenium specifically because of GitHub's security measures, and because of the high amount of state involved in building the request correctly.