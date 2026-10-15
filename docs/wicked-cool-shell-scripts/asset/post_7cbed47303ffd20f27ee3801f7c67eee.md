
```
while [ $tempyear -lt $endyear ] ; do
daysbetweenyears=$(($daysbetweenyears + \
  $(date -d "12/31/$tempyear" +%j)))
tempyear=$(($tempyear + 1))
done

#### DAYS IN END YEAR
dayofyear=$(date --date $endmon/$endday/$endyear +%j)   # That's easy!

#### NOW ADD IT ALL UP

totaldays=$(($daysleftinyear + $daysbetweenyears + $dayofyear))
fi
echo "There are $totaldays days until the date $endmon/$endday/$endyear."
exit 0
```

Listing 15-5: The daysuntil1 script

## How It Works

As we’ve said, there’s a lot of overlap between the daysago script and this script, enough that you could probably combine them into one script and have conditionals test whether the user is requesting a date in the past or a date in the future. Most of the math here is simply the inverse of the math in the daysago script, looking ahead into the future instead of back into the past.

This script is a bit cleaner, however, because it considers a lot more error conditions before invoking the actual calculations. Take, for example, our favorite test at ①.

If someone tries to trick the script by specifying today’s date, this conditional will catch that and return "zero days" as its calculation.

## Running the Script

How many days until January 1, 2020? Listing 15-6 gives us the answer.

```
$ daysuntil 1 1 2020
There are 1321 days until the date 1/1/2020.
```

Listing 15-6: Running the daysuntil1 script with the first day of 2020

How many days until Christmas 2025?

```
$ daysuntil 12 25 2025
There are 3506 days until the date 12/25/2025.
```

Preparing for the tricentennial in the United States? Here’s how many days you have left:

```
$ daysuntil 7 4 2076
There are 21960 days until the date 7/4/2076.
```

Finally, given the following, odds are good we won't be here for the third millennium:

```
$ daysuntil 1 1 3000
```

There are 359259 days until the date 1/1/3000.

In Script #99 on page 330, we were able to determine what day of the week a given date fell on. Combining this functionality with that of the daysago and daysuntil scripts to get all the relevant information at once would be very useful.

## Turning On Developer Mode

Once you’ve enrolled in the Windows Insider Program and have the Anniversary version of Windows 10 installed, you’ll need to get into Developer mode. To start, go to Settings and search for “Developer mode.” The Use developer features section should come up here. From here, select Developer mode, as shown in Figure A-1.

![](img/4ffb1cc24a1b24b49254839643abedb2_373_0.png)

Figure A-1: Enabling Developer mode in Windows 10

When you select Developer mode, Windows might warn you that going into Developer mode may expose your device to harm. The warning is legit: going into Developer mode does put you at greater risk because you can inadvertently install programs from non-approved sites. However, if you can remain careful and vigilant, we encourage you to proceed so you can at least test out the bash system. After you click through the warning, Windows will download and install some additional software onto your computer. This takes a few minutes.

Next, you’ll have to go into the old-school, early Windows configuration area to enable the Windows Subsystem for Linux. (It’s very cool that Microsoft even has a subsystem for Linux!) Get there by searching for “Turn Windows Features On.” A window will open with a long list of services and features, all with check boxes (see Figure A-2).

Don’t uncheck anything; you only need to check Windows Subsystem for Linux (Beta). Then click OK.

Your Windows system will prompt you to restart to fully enable the Linux subsystem and the new developer tools. Do so.

Figure A-2: The Turn Windows features on or off window

## Installing Bash

Now you're ready to install bash from the command line! Old school, for sure. In the Start menu, search for "command prompt" and open a command window. Then simply enter bash and you'll be prompted to install the bash software on your PC, as shown in Figure A-3. Enter y and bash will start to download.

Figure A-3: Installing bash within the command line system on Windows 10

![](img/4ffb1cc24a1b24b49254839643abedb2_374_0.png)

![](img/4ffb1cc24a1b24b49254839643abedb2_374_1.png)
