Linux supports the concept of a current directory, which is the directory on which all file and directory commands operate. After you log in, for example, your current directory is the home directory. To see the current directory, type the `pwd` command.

To change the current directory, use the `cd` command. To change the current directory to `/usr/lib`, type the following:

```
```bash
cd /usr/lib
```
```

Then, to change the directory to the cups subdirectory in `/usr/lib`, type this command:

```
```bash
cd cups
```
```

Now, if you use the `pwd` command, that command shows `/usr/lib/cups` as the current directory.

These two examples show that you can refer to a directory’s name in two ways:

+   - **An absolute pathname** (such as `/usr/lib`) that specifies the exact directory in the directory tree
+   - **A relative directory name** (such as `cups`, which represents the cups subdirectory of the current directory, whatever that may be)

If you type `cd cups` in `/usr/lib`, the current directory changes to `/usr/lib/cups`. However, if you type the same command in `/home/naba`, the shell tries to change the current directory to `/home/naba/cups`.

![](bbox=[0.13, 0.623, 0.208, 0.694])

Use the `cd` command without any arguments to change the current directory back to your home directory. No matter where you are, typing **cd** at the shell prompt brings you back home!

![](bbox=[0.118, 0.701, 0.209, 0.77])

By the way, the tilde character (`~`) refers to your home directory. Thus the command `cd ~` also changes the current directory to your home directory. You can also refer to another user’s home directory by appending that user’s name to the tilde. Thus, `cd ~spiderman` changes the current directory to the home directory of spiderman.

![](bbox=[0.13, 0.798, 0.208, 0.866])

Wait, there’s more. A single dot (`.`) and two dots (`..`) — often referred to as dot-dot — (clever, huh!) also have special meanings. A single dot (`.`) indicates the current directory, whereas two dots (`..`) indicate the parent directory. For example, if the current directory is `/usr/share`, you go one level up to `/usr` by typing

```
```bash
cd ..
```
```