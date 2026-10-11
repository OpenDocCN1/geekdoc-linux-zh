![](bbox=[0.08, 0.09, 0.58, 0.26])

Resort. The resort’s web page uses JavaScript to show the new snow in either centimeters or inches, but the Lynx text output displays both values and their units.

To remove parts of a string variable, you can use `%%` to extract the first part of the string and `%%` to extract the last part of the string (as shown in Listing 1).

# # A Bash Web Scraping Project

To get excited before a family ski trip, I wanted to create a morning notification script that would show the new morning snow and the base snow.

To create the notification script (Listing 2), I used two passes with the Lynx utility. The first pass scrapes for new snow (shown in Figure 4) and then a second pass gets the new base snow (shown in Figure 1). The snow results are then passed as a string ($msg) to the `notify-send` utility [4], which posts the message to the workstation desktop (Figure 5). You can schedule this Bash script to run every morning using either `cron` or the `at` utility.

![](bbox=[0.06, 0.28, 0.58, 0.48])

# # Summary

Scraping web pages can be tricky, and the pages can change at anytime. For this reason, it is always best to check if an API is available before looking at web scraping.

Python with the Beautiful Soup library has been my go-to approach for web scraping, but it’s nice know that a simple Bash alternative is also available.

# # Info

+   1. Lynx: [https://lynx.invisible-island.net/](https://lynx.invisible-island.net/)
+   2. `curl`: [https://curl.se/](https://curl.se/)
+   3. html2text: [https://github.com/Alir3z4/html2text/](https://github.com/Alir3z4/html2text/)
+   4. `notify-send`: [https://delightlylinux.wordpress.com/2020/10/25/bash-show-notifications-from-scripts-using-notify-send/](https://delightlylinux.wordpress.com/2020/10/25/bash-show-notifications-from-scripts-using-notify-send/)

# # Author

You can investigate more neat projects by Pete Metcalfe and his daughters at [https://funprojects.blog.](https://funprojects.blog.)

```
# Listing 2: Bash Web Scraping Notification Script
```bash
01 #!/bin/bash
02 #
03 # skitrip.sh – show the Sunshine ski conditions in a notification
04 #
05 theurl="https://www.snow-forecast.com/resorts/Sunshine/6day/mid"
06
07 # Get the new snow depth
08 thestr=""New snow in Sunshine Village:"" 
09 result=$(lynx -dump "$theurl" | grep "${thestr}")
10 newsnow="${result%cm}" cm"
11
12 # Get the base
13 thestr="Top Lift:" 
14 base=$(lynx -dump "$theurl" | grep "${thestr}") 
15
16 # Show the results in a desktop notification, with 120 minute wait time
17 msg="$newsnow\nbase" 
18 icon="$HOME/Downloads/mountain.png"
19 notify-send -t 120000 -i "$icon" "Sunshine Ski Resort" "$msg"
```
```