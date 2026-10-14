The first file already exists in the /etc/bind folder. All you need to do is add two definitions to point to your zone and reverse lookup files. Here are the steps required to configure the named.conf.local file for your network:

+   1. Open the /etc/bind/named.conf.local file in a text editor. If you're working on the Ubuntu server, you'll need to use a command-line editor to do this. The vim editor is installed by default in Ubuntu server and should work fine:
+   
+   sudo vim /etc/bind/named.conf.local

+   2. Add a zone definition pointing to the zone configuration file. The zone definition defines the domain name, along with the type of DNS server (master) and the filename of the zone configuration file:
+   
+   zone "smallorg.org" {
+       type master;
+       file "/etc/bind/db.smallorg.org";
+   };
+   
+   The semicolons at the end of the lines are important—they signify the end of a line.

+   3. Add a zone definition pointing to the reverse lookup configuration file. The reverse lookup configuration uses the backward IP address format to define the network:
+   
+   zone "0.0.10.in-addr.arpa" {
+       type "master";
+       file "/etc/bind/db.10";
+   };
+   
+   Again, each line in the zone file must end with a semicolon.

+   4. Save the named.conf.local file and exit the text editor. The Vim command to save the file and exit the editor is ZZ.

Once you've updated the named.conf.local file, you're ready to create your zone configuration and reverse lookup configuration files. First, here are the steps for creating the zone configuration file:

+   1. Create a new file called /etc/bind/db.smallorg.org using a text editor. If you specify the filename in the vim command line, the vim editor will automatically create it for you:
+   
+   sudo vim /etc/bind/db.smallorg.org

+   2. Add an SOA record for your zone. The SOA record needs to name your DNS server, along with the email address of an administrator account (remember to place a dot in place of the @ sign in the email address, and also remember to place a dot at the end of your DNS server name). A sample looks like this:
+   
+   @ IN SOA testbox.smallorg.org. postmaster.smallorg.org. (
+   2008010151 ; serial, todays date + todays serial #
+   3600 ; refresh, seconds
+   1800 ; retry, seconds
+   604800 ; expire, seconds
+   3600 ) ; minimum, seconds