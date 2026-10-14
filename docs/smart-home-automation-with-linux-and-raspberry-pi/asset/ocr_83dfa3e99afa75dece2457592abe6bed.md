Every status command, except vstatus, issues its report to the standard output stream. In this way, it can be incorporated directly into a web page output or piped into announce:

netstatus: Calls the user tool $MINBASE/bin/ipcheck to determine whether the external network is available, in addition to your local web server. Because ipcheck is synchronous, this can take a short while to happen, particularly if there’s no available Internet.

lstatus: Life status, reporting what should generally happen today. For example, “empty the bins tonight.” This is a housewide message and so appears on everyone’s status reports. It also accepts an (optional) argument to indicate a day of the week (0 meaning Sunday, 1 for Monday, and so on) or “tomorrow”.

weatherstatus: A simple echo of the weather forecast that has been downloaded and processed previously with ~minerva/update/weather.

mstatus: Reports on the media currently playing, including both MP3 and CDs, detailing the artist and album when they’re known.

status: All of the earlier reports are combined into one, along with the time and date, making it an informative alarm call.

tvnowon: Provides a list of the TV programs currently showing. The list is downloaded every night and stored locally, where this code rips out only those programs in the current time slot.

vstatus: A wrapper to status, presenting all the information in a spoken form with announce, meaning there’s a single chime at the beginning and end of the whole phrase, and not one between each individual report.

# Variable Constants

Although computers are very rigid devices, real life isn’t. The mantra/cliché of ’the only constant thing is change’ is true. So, as we saw when using the routine code to vary our alarm call, there are some tools which help with those things that always happen . . . but we just don’t know when they happen.

easter: A short script that computes the date of Easter Sunday for the current year, in the form 31 March 2013. If Easter has passed (which can be determined by passing the single argument ispassed) you can determine the date for the subsequent year and call easter $(('date +%Y' + 1))

sunrise: The time of sunrise, at your current location, in the form 06:35. This is good for affecting the lights around the house, particularly if your work means you’re getting up before sunrise, and want your lights to brighten naturally in the morning. You can specify your location with longitude and latitude coordinates in the file /usr/local/minerva/etc/location.inc.

sunset: The opposite of sunrise, obviously, with your current location specified in the same file.