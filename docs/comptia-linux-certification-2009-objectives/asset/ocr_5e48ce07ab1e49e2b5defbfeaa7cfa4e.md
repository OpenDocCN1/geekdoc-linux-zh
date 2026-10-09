+   2. Enter the NS and A records for the forward zone.

+   3. Create a zone file for the reverse domain resolution.

+   4. Specify global configuration options and zone statements for the root and loopback domains in the named.conf file.

+   5. Add zone statements for the forward and reverse zones.

+   6. Start the named service.

+   7. Add DNS name server data to the /etc/resolv.conf file on srvA.

+   8. Check whether the DNS server resolves hostnames and IP addresses.

# Lesson 12 Lab 2

# Configuring FTP Services

**Data Files:**
software-1, software-2, software-3, sourcecode-1.pl, sourcecode-2.pl, sourcecode-3.pl

+   **Before You Begin:**
To complete this lab activity, you need to perform the following tasks on srvB:
1. Create the users laura, linda, and miller.
2. Create a directory named /mnt/software_files and copy the files software-1, software-2, and software-3 from the /085039Data/Configuring_Network directory to the /mnt/software_files directory.
3. Create a directory named /sourcecode and copy the files sourcecode-1.pl, sourcecode-21.pl, and sourcecode-3.pl from the /085039Data/Configuring_Network directory to the /sourcecode directory.

**Scenario:**
You are a network administrator in OGC Systems. You want to enable teams in various locations to transfer files among each other. You need to ensure that only the required number of users can access the service.

> You can find a suggested solution for this activity in the Lesson 12 Lab 2 solution.html file in the Configuring_Network/Solution folder in the student data files.