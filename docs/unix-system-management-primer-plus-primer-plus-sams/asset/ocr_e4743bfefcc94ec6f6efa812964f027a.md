# Chapter 13 • IMPLEMENTING SYSTEM SECURITY

# Make a Permanent Copy of the Evidence

If possible, you should make a hard copy of any evidence or burn it to a CD-ROM. You might need such a permanent copy of the evidence later, for legal purposes.

# Reporting the Incident

At this point, you should take some time to report the incident to your local security administrator, who should be designated in your security policy (you learn about security policies in Chapter 16, "Computing Policies and Agreements"). If your organization isn't large enough to warrant a security administrator, report the incident to your manager and CTO or CIO. You might also consider reporting the incident to the CERT® (Computer Emergency Response Team) Coordination Center, which collects statistics on current and past security incidents. Those reports can help investigators track down the instigator of the attack. A form for report can be found at http://www.cert.org/reporting/incident_form.txt.

# Internal Response Teams

Universities and other large organizations may choose to form their own CERT-like organization to deal with their security issues internally before utilizing external resources.

# Backing Up System Data

Back up any critical system data and configurations onto tape or CD-ROM and mark it as quarantined or tainted data. You may need to retrieve an old configuration from this backup to re-create the compromised system.

# Don't Copy Tainted Data!

Never directly copy a file from a quarantined system or backup! You run the risk of tainting a system with potentially harmful configurations. Retype any configurations by hand instance.

# Reloading the Compromised Systems

Once a system has been compromised, it should be considered dead for all intents and purposes. Never reinsert a compromised system back into production! Wipe its disks clean and reload the operating system from scratch to eliminate any remaining damage from that system. Then, apply any patches or configuration changes necessary to plug up the hole that allowed the compromise in the first place.

You also should take some time to analyze what allowed the break-in to occur in the first place and implement new practices to ensure it does not happen again. For example, if your system was compromised because you neglected to install the latest security patches announced the month before, you could make it policy that all security patches should be tested and installed within a week of their announcement.