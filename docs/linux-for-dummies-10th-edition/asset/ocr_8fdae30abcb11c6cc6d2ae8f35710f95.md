# # Where the computer is the /usr

The /usr directory is often referred to as its own miniature filesystem tree. This directory has lots of important or interesting subdirectories, as shown in Table 7-2. An asterisk (\*) at the end of a description indicates that you need to leave that directory alone unless you have good reason to mess with it — after you gain lots of experience with Linux and know exactly what changes you need to make — so that you don’t accidentally alter something your system needs to function correctly. An interesting thing to remember about this section of the filesystem is that many advanced Linux users often use /usr to store programs that can be shared with other Linux machines.

**TABLE 7-2** Standard /usr Subdirectories

| Subdirectory | Contents |
| :----------- | :------- |
| /usr/bin | The commands that aren’t essential for users but are useful\* |
| /usr/games | The games that you install on your system, except for those that you can choose to place in /opt. |
| /usr/include | The files that the C programming language needs for the system and its programs\* |
| /usr/lib | The shared code used by many of the programs in this /usr subhierarchy\* |
| /usr/local | The programs and other items that you want to keep locally, even if you’re sharing everything else in /usr |
| /usr/sbin | The commands that aren’t essential for Administrators but are useful\* |
| /usr/share | The information that you can use on any Linux machine, even if it’s running incredibly different hardware from what this one is running\* |


# # Managing Your Filesystem without a Net (or Mouse)

Chapter 8 covers how to use the point–and–click file managers to work your way around the Linux filesystem. In this section, I take a look at how to use the command–line tools to find your way around the filesystem. It isn’t vital for you to know this, but it could certainly prove useful someday!