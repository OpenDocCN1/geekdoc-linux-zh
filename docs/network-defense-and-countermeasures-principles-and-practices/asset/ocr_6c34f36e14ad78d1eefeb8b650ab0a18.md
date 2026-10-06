# Understanding and Implementing Honeypots

In all modes, Specter logs the activity, including all information it can derive from the incoming packets. It also attempts to leave traces on the attacker's machine, which can provide clear evidence civil or criminal action later be required.

Users can also configure a fake password file in all modes. These are particularly useful because most hackers attempt to access a password file to crack the passwords. If they are successful they can log on as a legitimate user. The holy grail of hacking is getting the administrator's password. There are many ways to configure this fake password file:

+   **Easy**: In this mode the passwords are easy to crack, leading a wo-intruder to believe that she has actually created passwords and usernames. Often a hacker with a legitimate logon will be less careful covering her tracks. If you know that logon is fake and the system is set up to monitor it, you can track it back to the hacker.

+   **Normal**: This mode has slightly more difficult passwords to crack than the easy mode.

+   **Hard**: This mode has even harder passwords to crack. There is even tougher version of this mode called mean, which means the passwords are very difficult to break so that the hacker can be traced while he is taking time to crack the passwords.

+   **Fun**: This mode uses famous names as usernames. In my opinion this one, and the related one named Chebyshev, have dubious security value.

+   **Warning**: In this mode the hacker gets a warning telling him he has been detected if he is able to crack the password file. The theory behind this mode is that most hackers are simply trying to see if they can crack a system and do not have a specific objective. Letting this sort of hacker know he has been detected is enough to scare him off.

The cost of this software system is $900, and it requires a PC to install it. The purpose of honeypots like Specter is not preventing intrusion. Instead, they minimize the damage once someone is in. They serve to the hacker's attention away from critical systems. They can also be very helpful in tracking down hackers.

# Symantec Decoy Server

Because Symantec is a prominent vendor for both antivirus and firewall solutions, it should come as no surprise that it also has a honeypot solution. The first Symantec honeypot product was Decoy Server. It simulated being a real server by simulating many server functions, such as incoming and outgoing e-mail. You can learn full details about this product from Symantec, however, their product line and web page changes. The best way to find out about their honeypots is just to go to Symantec's main site and perform a search.