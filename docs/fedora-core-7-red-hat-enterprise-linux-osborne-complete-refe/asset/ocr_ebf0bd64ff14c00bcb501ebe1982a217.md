| Web Site | Tools |
| :--- | :--- |
| **rsync.samba.org** | rsync remote copy backup |
| **www.amanda.org** | Amanda network backup |
| **dump.sourceforge.net** | dump and restore tools |

**TABLE 34-1 Backup Resources**

If, instead, you wanted to preserve the ownership and permissions of the files, you would use the **-a** (archive) option. Adding a **-z** option will compress the file. The **-v** option provides a verbose mode.

```
`rsync -avz /home/george/myproject rabbit:/backup`
```

A trailing slash on the source will copy the contents of the directory, rather than generating a subdirectory of that name. Here the contents of the **myproject** directory are copied to the **george-project** directory.

```
`rsync -avz /home/george/myproject/ rabbit:/backup/george-project`
```

The **rsync** command is configured to use SSH remote shell by default. You can specify it or an alternate remote shell to use with the **-e** option. For secure transmission you can encrypt the copy operation with ssh. Either use the **-e ssh** option or set the **RSYNC_RSH** variable to ssh.

```
`rsync -avz -e ssh /home/george/myproject rabbit:/backup/myproject`
```

As when using **rcp**, you can copy from a remote host to the one you are on.

```
`rsync -avz lizard:/home/mark/mypics/ /pic-archive/markpics`
```

You can also run rsync as a server daemon. This will allow remote users to sync copies of files on your system with versions on their own, transferring only changed files rather than entire directories. Many mirror and software FTP sites operate as rsync servers, letting you update files without having to download the full versions again. Configuration information for rsync as a server is kept in the */etc/rsyncd.conf* file. On Fedora, rsync as a server is managed through **xinetd**, using the */etc/xinetd.d/rsync* file, which starts rsync with the **-e -daemon** option. In the */etc/services* file, it is listed to run on port 873. It is off by default, but you can enable it with system-config-services On Demand Services panel or **chkconfig**.

```
`chkconfig rsync on`
```

> **TIP** *Though it is designed for copying between hosts, you can also use rsync to make copies within your own system, usually to a directory in another partition or hard drive. In fact there are eight different ways of using rsync. Check the rsync Man page for detailed descriptions of each.*