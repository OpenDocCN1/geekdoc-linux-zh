# v.4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

We've all heard the ever famous "Trojan Horse Defense", where we worry malicious activity will be blamed on an infected computer that the defendant "had no control over". It is nothing I've personally experienced, it has happened and is well documented. Scanning the evidence makes sense from both an incriminatory and exculpatory point of view. If there are circumstances where malware may have played a role, we will want to know that.

There are other considerations that warrant a virus/malware scan, and it can very specifically depend on the type of case you are investigating. Simply making a check list for analysis is fine, but you must still have an understanding of why the scan is done, and how it applies to the case. For example, if the media being examined is the victim of compromise, then a virus scan provide a starting point for additional analysis. The starting point can be as simple as identifying a vector, and utilizing file dates and times to drive additional analysis. Alternatively, we may find ourselves examining the computer in a child exploitation case. Negative results, while presumptive, can still help to combat the previously discussed Trojan Horse Defense. The bottom line is that simple virus scan should always be included as standard practice. And while there are plenty of tools that could be compatible with Linux, we focus on ClamAV.

ClamAV is open source and available. It is well supported and is quite comparable to other anti-virus with respect to identifying infections and artifacts. If you are deploying ClamAV in a laboratory environment, it also provides excellent backup and cross-verification to anti-virus results provided in other operating systems.

We already installed the ClamAV package earlier in the section on software. If you have not done so, install clam via the SlackBuild (using sboinstall) or via your distribution's package management method.

ClamAV has far more use and configuration options that we will not cover here. It can be used to scan "on use" volumes, email servers, and has options for "safe browsing". There are tools installed with the ClamAV package that allow for byte code review, submission of samples, and test with daemon mode configuration. We will be using it to scan acquired evidence. This assumes we update it as needed and run on targeted image files, volumes or mount points. With our simplified use case, we will concentrate on two specific clam tools: freshclam and clamscan.

Once clam is installed, we will need to download the definition files. We do this with freshclam. This command will download the appropriate files with the initial main.cvd, as well as the daily cvd containing the most recent dates:

```
root@forensic1:~ freshclam
ClamAV update process started at Wed May 31 12:53:56 2017
WARNING: [LibClamAV] cl_cvdhead: Can't read cvd header in main.cvd
Downloading main.cvd [100%]
```

> http://digitalcommons.lsc.edu/cgi/viewcontent.cgi?article=1370&context=chtli

167