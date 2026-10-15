```
thedat="$1 # No error checking = dangerous
fi
url="http://www.moongiant.com/phase/$thedat"
pattern="Illumination:"
phase="$(curl -s "$url" | grep "$pattern" | tr ',' '\' | grep "$pattern" | sed 's/[^0-9]/g/')"
# Site output format is "Illumination: <span>NN%\n\n</span>"
if [ "$thedat" = "today" ] ; then
echo "Today the moon is ${phase}% illuminated."
else
echo "On $thedat the moon = ${phase}% illuminated."
fi
exit 0
```

Listing B-5: The moonphase script

# How It Works

As with other scripts that scrape values from a web query, the moonphase script revolves around identifying the format of different query URLs and pulling the specific value from the resultant HTML data stream.

Analysis of the site shows that there are two types of URLs: one that specifies the current date, simply structured as "phase/today", and one that specifies a date in the past or future in the format MM/DD/YYYY, like "phase/08/03/2017".

Specify a date in the right format and you can get the phase of the moon on that date. But we can't just append the date to the site's domain name without some error-checking, so the script splits the user input into three fields—month, day, and year—and then makes sure that the day and year values are nonzero at 1. There's more error-checking that can be done, which we'll explore in "Hacking the Script."

The trickiest part of any scraper script is properly identifying the pattern that lets you extract the desired data. In the moonphase script, that's specified at 2. The longest and most complicated line is at 3, where the script gets the page from the moongiant.com site, and then uses a sequence of grep and sed commands to pull just the line that matches the pattern specified.

After that, it's just a matter of displaying the illumination level, either for today or the specified date, using the final if/then/else statement.

# Running the Script

Without an argument, the moonphase script shows the percentage of lunar illumination for the current date. Specify any date in the past or future by entering MM/DD/YYYY, as shown in Listing B-6.