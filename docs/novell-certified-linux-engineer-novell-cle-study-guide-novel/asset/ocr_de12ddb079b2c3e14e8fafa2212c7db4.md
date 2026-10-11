> **NOTE** The directory services we are discussing here are those that are based on the X.500 directory service standard. You may hear these types of directories referred to as *full-service directories*. Many software vendors over the years have tried to pass off their flat-file user databases as "directories."

The first time I heard the term *directory*, back in the mid-1990s, the image of a phone book came to my mind. That analogy isn't far off. A full-service directory, however, can store more than just user information.

Let's take a few steps back into history. Recall that in an earlier chapter I related a story about my first networking job where I was responsible for an organization's NetWare 3 network.

NetWare 3 (and earlier versions of NetWare as well) used a flat-file database called the *bindery* to store user accounts and groups. Each server in my network had its own bindery. My organization had about 1200 users, each with his or her own account. Each needed access to resources hosted by each of the NetWare servers I was responsible for.

That required me to keep the user accounts and passwords synchronized on all servers in the organization. Needless to say, for the first couple of months on the job, that's about all I did. My users simply expected to have a single password to access all network resources.

If they changed their password in one bindery user account, they expected that password to work when accessing other servers in the network. Eventually, that would be so, but only after I fielded their complaint and manually changed the account information on the other servers.

After a couple of months, I became very annoyed with the situation and wrote some nifty little programs that could be used to synchronize accounts between servers; but it was still a manual process. If I forgot to run them, the accounts would quickly go out of sync and the help desk calls would start rolling in.

This situation also presented a problem when a new individual would join or leave the organization. I had to either create multiple accounts or delete multiple accounts on all the servers.

In addition, each version of the user's account had different trustee assignments and login scripts. Talk about job security.

If you've ever managed a Linux network that employed multiple servers, you've faced a similar issue. Remember that Linux users and groups are