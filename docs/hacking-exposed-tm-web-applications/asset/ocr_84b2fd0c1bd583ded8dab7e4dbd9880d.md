# # Chapter 3: Hacking Web Servers

We’re going to admit up front that we have not actually touched the latest version of AppScan from Sanctum, Inc. However, we have reviewed the information on the product posted by Sanctum, and we have discussed it with users and those who have reviewed the product for trade magazines and their own companies. By most accounts, it appears to be a Web Application security scanner that checks for a wide array of vulnerabilities that are researched in Sanctum's own labs. Data output from the product can be imported into multiple formats, and some built-in spashly, graphical HTML reports are available as well. Custom vulnerability checks can be created based on existing checks from within the application, or developed from scratch using the “Manual audit” feature.

However, AppScan comes at a very dear price, starting at $15,000 per seat per year. And don’t think you’re going to find a pirated copy on the Web—the program is registered to the system on which it runs through hardware features like the disk drive ID, and it will not operate if copied or moved

# FoundScan Web Module

| | |
|---|---|
| Pro: | Comprehensive checks: content harvesting and analysis, smart guesswork, authentication attacks including NTLM, SQL attacks |
| Con: | Available largely as a managed service of this writing; packaged version requires IIS and SSL (free Desktop Edition is OK) to operate |
| Final Analysis: | No comment |

Before we discuss FoundScan’s Web Module, we should note that the authors are shareholders in Foundation, Inc., makers of the tool (hence the “no comment” above). OK, now that full disclosures have been made, let’s state right off that FoundScan is quite different from shrink-wrapped tools we have discussed so far. As of this writing, it is only available as a managed vulnerability assessment service, which is, briefly, a 24X765 vulnerability scanner run from Foundation’s Secure Operations Center (SOC) over Internet-accessible hosts. The availability of FoundScan as a packaged enterprise product was announced in April 2002, with installation available to customers soon thereafter.

The Web Module is an optional component of the FoundScan service. In addition to the many network and operating system-level vulnerability checks performed by the basic FoundScan, the Web Module enumerates all Web servers and banners (even over SSL); analyzes all Web server content; identifies basic, digest, and NTLM authentication points and attempts limited credential guessing; performs “smart guesswork” to discover common Web application weaknesses such the location of unindexed include files; attempts exploitation of common source code disclosure issues; and analyzes