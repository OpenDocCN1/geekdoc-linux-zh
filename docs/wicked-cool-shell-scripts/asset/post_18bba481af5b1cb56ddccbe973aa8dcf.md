
```
awk '(print $11) "$1" | \
grep -vE "(^\.|$|www.$host/$host)" | \
sort | uniq -c | sort -rn | head -10
echo ""
exit 0
```

Listing 10-1: The webaccess script

## How It Works

Let's consider each block as a separate little script. For example, the first few lines extract the firstdate and lastdate ① by simply grabbing the fourth field of the first and last lines of the file. The number of hits is calculated by counting lines in the file using wc ②, and the number of page views is calculated by simply subtracting requests for image files (that is, files with .gif, .jpg, or .png as their extension) from the hits. Total bytes transferred are calculated by summing up the value of the 10th field in each line and then invoking nice number to present it attractively.

To calculate the most popular pages, first we extract just the pages requested from the log file, and then we screen out any image files ③. Next we use uniq -c to sort and calculate the number of occurrences of each unique line. Finally, we sort one more time to ensure that the most commonly occurring lines are presented first. In the code, this whole process is at ④.

Notice that we do normalize things a little bit: the sed invocation strips out any trailing slashes to ensure that /subdir/ and /subdir are counted as the same request.

Similar to the section that retrieves the 10 most requested pages, the section at ⑤ pulls out the referrer information. This extracts field 11 from the log file, screening out entries that were referred from the current host as well as entries that are "-", the value sent when the web browser is blocking referrer data. Then the code feeds the result to the same sequence of sort|uniq -c|sort -rn|head -10 to get the 10 most common referrers.

## Running the Script

To run this script, specify the name of an Apache (or other Common Log Format) log file as its only argument.

## The Results

The result of running this script on a typical log file is quite informative, as Listing 10-2 shows.

```
$ webaccess /web/logs/intuitive/access_log
Results of analyzing log file access_log

Start date: 01/May/2016 at 07:04:49
End date: 04/May/2016 at 01:39:04
```

Hits: 7,839 (total accesses)
Pageviews: 2,308 (hits minus graphics)
Transferred: 25,928,872,755 bytes

The 10 most popular pages were:

- 266
- 118 /CsharpVulnJson.ova
- 92 /favicon.ico
- 86 /robots.txt
- 57 /software
- 53 /css/style.css
- 29 /2015/07/01/advanced-afl-usage.html
- 24 /opendiagnostics/index.php/OpenDiagnostics_Live_CD
- 20 /CsharpVulnSoap.ova
- 15 /content/opendiagnostics-live-cd

The 10 most common referrer URLs were:

- 108 "https://www.vulnhub.com/entry/csharp-vulnjson,134/4"
- 33 "http://volatilminds.net/2015/07/01/advanced-afl-usage.html"
- 32 "http://volatilminds.net/"
- 15 "http://www.volatilminds.net/"
- 14 "http://volatilminds.net/2015/06/29/basic-afl-usage.html"
- 13 "https://www.google.com/"
- 10 "http://livedvdlist.com/opendiagnostics-live-cd"
- 10 "http://keywords-monitoring.com/try.php?u=http://volatilminds.net"
- 8 "http://www.volatilminds.net/index.php/OpenDiagnostics_Live_CD"
- 8 "http://www.volatilminds.net/blog/"

Listing 10-2: Running the webaccess script on an Apache access log

## Hacking the Script

One challenge of analyzing Apache log files is that there are situations in which two different URLs refer to the same page; for example, /custer/ and /custer/index.html are the same page. Calculating the 10 most popular pages should take this into account. The conversion performed by the sed invocation already ensures that /custer and /custer/ aren’t treated separately, but knowing the default filename for a given directory might be a bit trickier (especially since this can be a special configuration on the web server).

You can make the 10 most popular referrers more useful by trimming referrer URLs to just the base domain name (e.g., slashdot.org). Script #74, coming up next, explores additional information available from the referrer field. The next time your website gets "slashdotted," you should have no excuse for not knowing!

## #74 Understanding Search Engine Traffic

Script #73 can offer a broad overview of some of the search engine queries that point to your site, but further analysis can reveal not only which search engines are delivering traffic but also what keywords were entered by users who arrived at your site via search engines. This
