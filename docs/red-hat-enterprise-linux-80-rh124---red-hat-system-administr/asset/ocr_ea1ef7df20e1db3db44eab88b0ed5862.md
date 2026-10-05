When the server is unplugged, the operating system fails to continue.

+   1 Urgent
2 High
3 Normal
4 Low

Please select a severity (or 'q' to exit): **4**
Would you like to assign a case group to this case (y/N)? N
Would you see if there is a solution to this problem before opening a support case?
(y/N) N

Support case 01034421 has successfully opened.

If the --product and --version options are not specified the **redhat-support-tool** provides a list of choices for those options.

```
[user@host ~]$ redhat-support-tool
Welcome to the Red Hat Support Tool.
Command (? for help): opcase
Do you want to use the default product - "Red Hat Enterprise Linux" (y/N)?: y
output omitted...
29 7.5
31 7.6
32 8.0 Beta
```

Please select a version (or 'q' to exit): **yum fails to install apache**
Please enter a description (Ctrl-D on an empty line when complete):
yum cannot find correct repo

+   1 Urgent
2 High
3 Normal
4 Low

Please select a severity (or 'q' to exit): **4**
Would you like to use the default (Ungrouped) Case Group (y/N)?: y
Would you like to see if there is a solution to this problem before opening a support case? (y/N) N

Support case 018355678 has successfully opened.

# # Attaching Diagnostic Information to a Support Case

Including diagnostic information can lead to a quicker resolution. Attach the **sosreport** when the case is opened. The **sosreport** command generates a compressed archive of diagnostic information gathered from the running system. The **redhat-support-tool** prompts to include one if an archive has been created:

> Please attach a SOS report to support case 01034421. Create a SOS report as the root user and execute the following command -c sosreport directly to the case:
redhat-support-tool attachment -c 01034421 path to sosreport

Would you like to attach a file to 01034421 at this time? (y/N) N
Command (? for help):