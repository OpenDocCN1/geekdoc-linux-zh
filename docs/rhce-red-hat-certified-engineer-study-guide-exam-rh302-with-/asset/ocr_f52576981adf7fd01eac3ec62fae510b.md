# less

The less command lets you page through a text file much as the man command lets you page through a man page. You use the same characters to control both programs. For example, to page through the file /etc/hosts, issue the command

```
less /etc/hosts
```

# ls

The ls command lists files and their characteristics. It has many options and arguments; this section describes only the most commonly used. Without using any options or arguments, the ls command lists the names of files residing in the current directory. If you want to list some directory, issue a command as

```
ls /home/bob
```

which lists the names of files residing in the directory /home/bob. You might, for example, see output like this:

Desktop My Documents Sara.wab WAB.EXE sara.blt sounds

As explained later, this command will give you an error message if you lack the appropriate permissions to access the specified directory. An important option of the ls command causes to list the characteristics of the files along with their names. For example, the command

```
ls -1 /home/bob
```

might produce output like this:

| total 137 |
| drwxr-xr-x 5 bob bob 1024 Nov 26 10:35 Desktop |
| drwxr-xr-x 14 bob bob 1024 Nov 26 10:38 My Desktop |
| -rwxrxr-- 1 bob bob 115030 Nov 26 13:15 Sara.wab |
| -rwxrxr-- 1 bob bob 14768 Mar 13 19:57 WAB.EXE |
| -rwxrxr-- 1 bob bob 2089 Nov 26 10:36 sara.blt |
| drwxr-xr-x 2 bob bob 2048 Nov 26 10:39 sounds |

The first line tells you that the files in the /home/bob directory occupy a total of 137 blocks of disk space. Each subsequent line describes one of the files.