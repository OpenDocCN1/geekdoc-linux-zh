[Enter]. The installation program attempts to guess your **Netmask** based on your IP address; you may change the netmask if it is incorrect. Press [Enter]. The installation program guesses the **Default gateway** and **Primary nameserver** addresses from your IP address and netmask; you may change them if they are incorrect. Choose **OK** to continue.

The second dialog prompts you for a domain name, a hostname, and other networking information (see Figure 2.7). Enter the **Domain name** for your system and press [Enter]; the installation program carries the domain name down to the **Host name** field. Enter the hostname you are using in front of the domain name to form a fully qualified domain name (FQDN). If your network has more than one nameserver, you may enter IP addresses for additional nameservers in the **Secondary nameserver** and **Tertiary nameserver** fields. Choose **OK** to continue.

# FTP Server Information

If you're installing via FTP, the next dialog requests information about the FTP server (see Figure 2.10). Enter the name or IP address of the FTP site you are installing from, and the name of the directory there which contains the RedHat directory for your architecture. For example, if the FTP site contains the directory */pub/mirrors/redhat/1386/RedHat*, enter */pub/mirrors/redhat/1386*. If you are not using anonymous FTP, or if you need to use a proxy FTP server (if you're behind a firewall, for example), another dialog requests the FTP account or proxy information.

# SMB Server Information

If you're installing via SMB volume, the next dialog requests information about the SMB server (see Figure 2.11). Enter the name or IP address of your SMB server, the name of the shared volume which contains the Red Hat Linux CD, and the account name and password for the volume.

# 2.4.9 Creating Partitions for Red Hat Linux

After choosing whether to use SCSI support (and, if you're installing via FTP, after you configure networking information), the installation program presents a list of the hard disks it can find on your system and prompts you