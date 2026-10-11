During the configuration of the scan definition, we did not configure any credentials, which implies that this scan will run unauthenticated. Additionally, we accepted the defaults under **Basic Network Scan**, which means brute forcing of user credentials will not be enabled. If we review other options under **Basic Network Scan**, we can verify that the scan will run generic checks against the target in contrast to other templates like **Spectre and Meltdown**, which include specific vulnerability checks. Keep in mind that a scan configured like this will be highly noticeable on the network traffic level as it scans all ports and searches for all applicable vulnerabilities.

Now that we have completely reviewed all the configuration options and understand (at least at a high level) what the scanner is going to do, we can proceed with running our first scan.

# 8.2.4 Unauthenticated Scanning With Nessus

When we are ready to run this first unauthenticated scan, we click the arrow next to Save and then click Launch:

![](bbox=[0.28, 0.35, 0.72, 0.59])

*Figure 60: Launching the Scan*

Initially, the scan will have a status of *Running* (Figure 61).

![](bbox=[0.14, 0.65, 0.88, 0.81])

*Figure 61: Scan Status in Progress*

Once the scan is finished, the status will change to *Completed* (Figure 62).