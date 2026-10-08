You can obtain a listing of the files and directories in your own top-level directory by using the ls -C -F / command. (You'll learn all about the ls command in the next hour. For now, just be sure that you enter what's shown in the example.)

On a different computer system, here's what I see when I enter that command:

```
$ ls -C /
Mail/ export/ public/
News/     home/    reviews/
add_swap/ kad*    sbin/
apps/     layout   sys/
archives/ Lib*    ftftpboot/
bin@     found+  usr/
boot     mnt/      utilities/
cdron    net/      var/
chess/   ntpserver vminix*
dev/      /pcsfs/
```

In this example, any file that ends with a slash (/) is a folder (UNIX calls such directories). In this example any file that ends with an asterisk (*) is a program. Anything ending with a sign (@) is a symbolic link, and everything else is a normal, plain file.

As you can see from these two examples, and as you'll quickly find when you try to organize the top-level directory, there is much variation in how different UNIX systems organize the directories. There are many directories and files in common, and once you start examining the contents of specific directories, you'll find hundreds of programs and files show up in the same place from UNIX to UNIX.

It's as if you were working as a file clerk at a new law firm. Although this might have a specific approach to filing information, the approach may be similar to the filing system of other firms where you have worked in the past. If you know the underlying organization, you can quickly pick the specifics of a particular organization.

> Try the command ls -C -F / on your computer system, and identify, as previously explained, the directories in your result listing.

> The output of the ls command shows the files and directories in the top level of your system. Next, you learn what they are.

# The bin Directory

In UNIX parlance, programs are considered executables because users can execute them. (In this case, execute is a synonym for run, not an indication that you want to wander about murdering innocent applications!) When the program has been compiled (usually from a C listing), it is translated into what's called a binary format. Add the two together, and you have a common UNIX description for an application—an executable binary.

![](bbox=[0.063, 0.874, 0.135, 0.966])