
**Figure 15.1** Using FTP to transfer files from a remote system.

![](img/415c89a1ede71e11e5040a0038b6916c_636_0.png)

Another useful feature of FTP is the ability to send a group of files at one time through the use of the `mput` and `mget` commands. These commands allow you to give a single file name, a wildcard file name, or no file name at all. Through the use of `mput` and `mget`, you can quickly transfer an entire directory as shown in Figure 15.2, and, by using the `prompt` command, you can bypass the interactive questioning that is on by default in FTP. Figure 15.3 shows the advantage of using the `mget` command with the functionality of the `prompt` command.

Table 15.3 highlights some of the pros and cons of using FTP for software management. On the plus side, FTP provides a secure, password-protected method that provides a simple mechanism for transferring files between two distinct systems. However, if you need to distribute files to a large number of systems, the process is highly manual and very time-intensive. You are also limited to transferring files only from the current directories, so if you have a large directory tree to transfer, you’ll spend a great deal of time typing the `cd` command.

> FTP provides a mechanism to transfer files from one system to another where a direct filesystem copy is not an option. FTP is used to transfer software packages, image files, and user data.

**Figure 15.2** Using mget to speed file transfer.

![](img/415c89a1ede71e11e5040a0038b6916c_637_0.png)

**Figure 15.3** Using mget and prompt to automate transfers.

![](img/415c89a1ede71e11e5040a0038b6916c_637_1.png)

**Table 15.3 Pros and Cons of FTP Usage for Software Management**

| Pros | Cons |
|---|---|
| Simple Machine-to-machine Transfer | Highly manual |
| Password Protected | Does not scale well |
|  | Limited to a single directory; no recursion |

## Remote File Distribution

Since FTP is not an acceptable solution for managing a large volume of files and packages, another utility you should employ is the Remote File Distribution program `rdist`. The `rdist` program is designed to automatically replicate a directory structure from one system to another, without manual intervention. The `rdist` utility is highly effective at making replicas of existing file structures, like `/usr/local`, or archiving a copy of a file structure for redundancy. Figure 15.4 shows the file structure we wish to replicate from `mars.sniglets.com/home/local` to `earth.sniglets.com`, into `/export/local`. As you can see in Figure 15.5, `earth.sniglets.com` has nothing in `/export/local`. If we run `rdist` from mars, the complete file structure from mars is transferred to earth in `/export/local`.

![](img/415c89a1ede71e11e5040a0038b6916c_638_0.png)

![](img/415c89a1ede71e11e5040a0038b6916c_638_1.png)

**Figure 15.5** Using rdist to distribute files to a remote system.

![](img/415c89a1ede71e11e5040a0038b6916c_639_0.png)

In the example in Figure 15.5, we only added files to an existing file structure. Over time, if you continue to run `rdist` in this manner, you’ll eventually fill up the disk on earth, since by default, `rdist` only copies additions to the remote system, and does not remove files that have been deleted from the local system. Figure 15.6 shows a directory on mars that has a new file, `foo4`. `foodir` has been deleted, but it still exists on earth. By using the `-R` option, which deletes files from the remote system that no longer exist on the local system, after `rdist` has completed, the directories will be exactly the same, as shown in Figure 15.7.

Using `rdist` is a simple and powerful way to manage directory structures that you want to replicate and keep synchronized. Table 15.4 shows the pros and cons of using `rdist`. The `rdist` program is highly configurable, keeps files perfectly synchronized, maintains ownership and access times, and doesn’t send passwords over the network like FTP. The only downside

**Figure 15.6** New directory structure, with a directory deleted and a new file added.

![](img/415c89a1ede71e11e5040a0038b6916c_639_1.png)
