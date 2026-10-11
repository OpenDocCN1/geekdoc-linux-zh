To do so, we right-click anywhere on the page and select *View Source*.

![](bbox=[0.13, 0.15, 0.88, 0.58])

While it is possible for Javascript to alter the DOM, resulting in the DOM and source being different, this does not seem to be the case here. The source and DOM are fairly similar.

Next, we will run a basic `dirb` scan to discover any potential hidden files. Jenkins will respond with a 403 for any file that we try to access when we are not logged in, so we will run our scan with the `-w` flag to continue scanning past the warning messages.

```
kali@kali:~$ proxychains dirb http://10.5.5.25:8080/ -w 
...
URL_BASE: http://10.5.5.25:8080/
WORDLIST_FILES: /usr/share/dirb/wordlists/common.txt
OPTION: Not Stopping on warning messages

-----------

GENERATED WORDS: 4612

---- Scanning URL: http://10.5.5.25:8080/ ----
|S-chain|<!--127.0.0.1:1080--><>--10.5.5.25:8080--><>-->OK
(!) WARNING: All responses for this directory seem to be CODE = 403.
(Use mode '-w' if you want to scan it anyway)
```