# NOTE: You do not need to add the root user.

If you make any mistakes while adding new users, you can also delete and edit them as well.

Click on Next to continue.

# Authentication Configuration

Linux keeps its list of users in the /etc/passwd file. Each system has its own copy of this file, and a user listed in one /etc/passwd cannot log into another system unless they have an entry in the other /etc/passwd file. To allow users to log into any system in a network of computers, Linux uses the Network Information System (NIS) to handle remote password file issues.

In addition to listing users, the /etc/passwd file contains all of the passwords for each user in an encrypted format. For a very long time, this was acceptable since the process of attacking such files to crack passwords was so computationally expensive, it was an almost futile thing to even try. Within the last few years, affordable PCs have gained the necessary computational power to present a threat with this type of security, and therefore a must to use shadow passwords has come. With shadow passwords, the actual encrypted password entry is not kept in the /etc/passwd file but rather in a /etc/shadow file. The /etc/passwd file remains readable by any user in the system, but /etc/shadow is readable only by the root user only. This is obviously a good step up in security, unless you have a specific reason not to do this, be sure to check the Shadow Passwords checkbox (see Figure 2-13).

Another good security trick is to use passwords encrypted with MD5. This algorithm supports longer passwords (256 characters instead of just 8) because it takes longer to compute the hash, it takes longer for crackers to attack your system should they try to do so.

If your site has an existing NIS infrastructure, enter the relevant NIS domain and server name in this window. If you don't know or if you want to deal with this later, you can safely Ignore this step.

Once you have selected all checkboxes and filled out the relevant entries, click on Next to continue to the next screen.

# Selecting Package Groups

This is where you can select what packages get installed onto the system. Red Hat categorizes these packages into several high-level descriptions, which allows us to make a quick selection of what type of packages you want installed and safely ignore the details. You can also select to install all of the packages that come with Red Hat; but be warned, a full install can be upwards of 1.5GB of software!

Looking at the choices (Figure 2-14), we see the menu of top-level groups that Red Hat gives us. We can simply pick the groups that interest us, we can pick Everything to make all of the packages installed; or we can click on a button at the bottom of the screen labeled "Select individual packages." Once we have made our decisions, we simply click on Next.