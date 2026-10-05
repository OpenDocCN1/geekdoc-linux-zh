# Password vaults and password escrow

Five hundred miles north of the Norwegian mainland, on the island of Spitzbergen, a huge vault has been tunnelled into the mountainside as a place for the world's countries to store seed samples against the possibility of future catastrophe. System administrators don't need a vault that is large or that for passwords, but they do not need a vault.

A password vault is a piece of software (or a combination of software and hardware) that stores passwords for your organization in a more secure fashion than “Would you like Windows to remember this password for you?” Several developers have made a password vault almost a necessity:

+   - The proliferation of passwords needed not just to log in computers, but also to access web pages, configure routers and firewalls, and administer services

+   - The increasing need for strong (read “not very memorable”) passwords as computers get so fast that weak passwords are easily broken

+   - Regulations that require access to certain data to be traceable by a single person—no logins as such

Password management systems are emerging in the wake of legislation in the United States that attempt to ensure accountability and security on business sectors. In some cases, this legislation requires two-factor authentication; for example, a password or passphrase plus a challenge/response exchange. Password vaults are also a great boon for sysadmin support who must secure and traceably manage passwords not only for their own machines but also for their customers' machines.

Several vault implementations are available. Free for individuals (e.g., KeepPass) store passwords locally, all-or-nothing access to the password database, and no logging. Appliances suitable for huge enterprises (e.g., CyberArk) can cost tens of thousands of dollars. Many of the commercial offerings charge either by the user or by the number of passwords they remember.

We use a home-grown web-based system that has several nice features. One of our favorites features is the “break the glass” option, named for the fire alarm stations that tell you to break the glass and pull the big red lever in the event of an emergency.

In this case,“breaking the glass” means obtaining a password that you wouldn't normally have access to. In the event of an emergency, you can go ahead and retrieve the password anyway. The system notifies a list of other sysadmins and logs what you do with the password. When you have finished dealing with the emergency, change the password and put the new password back in the vault.

A low-tech way to implement password escrow is to store passwords in tamper-evident, serial-numbered bag of the type used by police to hold crime scene