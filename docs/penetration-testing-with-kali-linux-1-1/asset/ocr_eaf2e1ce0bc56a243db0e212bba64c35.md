```
```powershell
kali@kali:~$ mkdir notes

kali@kali:~$ cd notes/

kali@kali:~/notes$ mkdir module one

kali@kali:~/notes$ ls
module  one

kali@kali:~/notes$ rm -rf module/ one/

kali@kali:~/notes$ mkdir "module one"

kali@kali:~/notes$ cd module\ one/

kali@kali:~/notes/module one$
```

```

We can create multiple directories at once with the incredibly useful `mkdir  -p`, which will also create any required parent directories. This can be combined with brace expansion to efficiently create a directory structure to, for example, store your penetration test notes. In the example below, we are creating a directory called **test** and within that directory, creating three sub-directories called **recon**, **exploit**, and **report**.

```
```powershell
kali@kali:~$ mkdir -p test/{recon,exploit,report}

kali@kali:~$ ls -l test/
exploit
recon
report
```
```

# ### 2.4.3 Finding Files in Kali Linux

Three of the most common Linux commands used to locate files in Kali Linux include `find`, `locate`, and `which`. These utilities have similarities, but work and return data in different ways and therefore may be used in different circumstances.

# #### 2.4.3.1  `which`

The **`which`** command <sup>39</sup> searches through the directories that are defined in the `$PATH` environment variable for a given file name. This variable contains a listing of directories that Kali searches when a command is issued without its path. If a match is found, **`which`** returns the full path to the file as shown below:

```
```shell
kali@kali:~$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin

kali@kali:~$ which sdb
/usr/bin/sdb
```
```

<sup>39</sup> (die.net, 2019), https://linux.die.net/man/1/which