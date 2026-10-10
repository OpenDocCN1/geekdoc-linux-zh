![](bbox=[0.13, 0.1, 0.9, 0.48])

Figure 10-2. Nessus report indicating the presence of /src/passwd.inc on a vulnerable web server

# SUMMARY

This chapter demonstrates the ease of writing plug-ins for the Nessus scanner using the NASL language. First, an example web application vulnerability was presented. Next, the creation of a NASL script to detect this vulnerability was discussed in detail, with step-by-step explanation of the script source code. Instructions on how to incorporate the NASL script into Nessus's list of plug-ins were also provided. Quite often, large organizations use home-grown software applications in which vulnerabilities may be discovered. In addition, the Nessus scanner package may not contain a vulnerability check whose detection may be vital to an organization's security posture. The information contained in this chapter can be used to write Nessus plug-ins from scratch in order to detect such vulnerabilities.