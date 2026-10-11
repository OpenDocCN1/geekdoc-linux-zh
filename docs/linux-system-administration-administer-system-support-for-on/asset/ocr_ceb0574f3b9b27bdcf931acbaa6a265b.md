Now, to run the scanner, press the Start Scan button. After the scanner runs, click Start Analysis and pick the type of reporting you want (consider the sample reports given here). Listing 9-3 shows a scan reporting the number of vulnerabilities per host and what types they are.

# Listing 9-3: Number of vulnerabilities per host

```
Internet Security Scanner (C)1992-1997
ISS SAFEsuite Version 4.3.8
By Internet Security Systems, Inc.
Analysis Report

Summary Report of Vulnerabilities
Summary Information
Hosts Scanned: 1
Hosts with Active Services: 1
Hosts with No Services: 0
Start Time: Tue Jul 7 15:40:21 1998
End Time: Tue Jul 7 15:44:12 1998
Total Time: 3 minutes 51 seconds
Scan Completed Normally

Total Number of Vulnerability Risks: 10
Average Number of Vulnerability Risks per Active Hosts: 10.00
```

The first part of the report is the total vulnerabilities and the average per host. Because we have one host we're scanning, the total should equal the average.

```
Maximum License Number Reached: 0
Out of Range: 0
Open Ports via Socks Service [High Risk]: 0
Open Defaults found through Telnet [High Risk]: 0
Open Defaults found through Rexec [High Risk]: 0
Open Defaults found through FTP [High Risk]: 0
Open Defaults found through POP3 [High Risk]: 0
Accounts accessible through Rsh [High Risk]: 0
X Check [High Risk]: 1
```

The first vulnerability it found was in X. Most vulnerabilities only have one common way to exploit them, so there will usually be one following the description if a risk is found.

```
Sendmail Vulnerable Version [High Risk]: 0
Udecode Alias in Sendmail [High Risk]: 0
Remote Execution Hole in Sendmail [High Risk]: 0
Wizard Backdoor in Sendmail [High Risk]: 0
```