The vulnerability scanner simply checks to see whether that file at **C:\Windows\system32\drivers** has been updated to srv2.sys. If it has been updated, the system is not vulnerable to the EternalBlue exploit and all the malware that uses it.

Serv.sys on Windows 7 system 99 | P a g e

In addition, vulnerability scanners check to see whether operating systems and applications are up to date on their patches.

# What are False Positives?

False positives are generated when a system such as a vulnerability scanner says something exists, but it does not. For instance, if your system vulnerability scanner says that your system is vulnerable to EternalBlue and it is not, that is a **false positive** . Unfortunately, vulnerability scanners are far from perfect and generate a lot of false positives.

False Positive

The scanner indicates the vulnerability exists (positive) and it doesn’t exist (false).

False Negative

The scanner indicates the vulnerability doesn’t exist (negative) and it does exist (true).

True Positive

The scanner indicates the vulnerability exists (positive) and it does exist (true).

True Negative