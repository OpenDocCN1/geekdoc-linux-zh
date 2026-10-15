# Finding Out Which Group You're In

If you want to collaborate on a project and share files, for example, you'll need to be in the same group with the other people on the team. Your first step is to find out which group you're in, as shown in Code Listing 5.3.

# To find out which group you're in:

+   1. grep yourid /etc/passwd
+   
+   Here, grep yourid pulls your userid out of the /etc/passwd file (which is where user information is stored) and displays it as shown in Code Listing 5.3. From left to right, you see
+   ▲ Your username
+   ▲ The encoded password (or nothing, or an x if the system is configured for "shadow" passwords)
+   ▲ Your userid (each user has a unique number in the system)

+   2. Note the number of the group.
+   You'll need the number to match it up with a group name in step 3. In this case, our group id is 500.

+   3. more /etc/group
+   
+   Here, we're exploring the contents of the /etc/group file using more to see which groups are currently defined on the system. As shown in Code Listing 5.4, the first column contains the name of the group, the third contains the group number, and the last column contains extra names the system administrator added to the group. Users can belong to multiple additional groups, and this is how the additional group membership is indicated.

+   4. Match up the group number for your ID with the group name.
+   Our number was 500, which corresponds to the ejr group name here.

```
[ejr@hobbes permissions]$ grep ejr /etc/passwd
ejr::oag2,lyCyJKEJNE:500:Eric J. Ray:/home/ejr:/bin/bash
[ejr@hobbes permissions]$
```

Code Listing 5-3 You'll find tons of information in /etc/passwd, including your default group number.

```
[ejr@hobbes permissions]$ cat /etc/group
knem::9:
wheel::10:root,ejr
mail::12:mail
news::13:news
uucp::14:uucp
man::15:
games::20:
gopher::30:
dip::40:
ftp::50:
nobody::99:
users::100:ejr,deb,osr,owr
floppy::x:19:
pppusers::x:230:
popusers::x:231:
slipusers::x:232:
postgres::x:233:
ejr::x:500:
bash::x:501:
csh::x:502:
osr::x:503:
owr::x:504:
deb::x:505:
[ejr@hobbes permissions]$
```

Code Listing 5-4 The group file lists groups and additional members (as shown in the users group).