![](bbox=[0.18, 0.12, 0.82, 0.48])

Figure 2-15 Select the correct time zone from the map or the text listing.

Part of protecting **root** means not allowing users to log in as the root user over the network. This keeps crackers from being able to guess your root password by using automated login scripts. In order to allow legitimate users to become the root user, you need to log in as yourself, and then use the **su** (switch user) command. Thus, setting the root password isn't enough if you intend to perform remote administration; you will need to set up a real user, as well.

In general, it is considered a good idea to set up a normal user to do day-to-day work anyway. This gives you the protection of not being able to accidentally break configuration files or other important components while you're just surf the Net or performing nonadministrative tasks. The exception to this rule is, of course, certain server configurations where there should never be any users besides the root user (for example, firewalls).

In Figure 2-16, you see the screen that lets you set the root password as well as create new users.

Begin by picking a root password and entering it into the **Root Password** box at the top of the screen. Enter it again in the **Confirm box** right below; this protects you from locking yourself out of the system in case you make a typo. The text **Root Password Accepted** will appear below the password boxes once you have entered a password twice the same way.