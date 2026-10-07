
```
barry@forensic1:-$ mmls NTFS_Part_2017/NTFS_Part_2017.E01
DOS Partition Table Offset: 0 Units are 512-byte sectors

| Slot | Start | End | Length | Description |
| :--- | :--- | :--- | :--- | :--- |
| 000: Meta | 00000000 | 00000000 | 0000001 | Primary Table (#0) |
| 001: | 00000000 | 00002047 | 2048 | Unallocated |
| 002: | 00002048 | 00002399 | 352 | NTFS / exFAT (0x07) |
```
```
barry@forensic1:-$ find -n "users/alberte/ntuser.dat" -o 2048 NTFS_Part_2017/NTFS_Part_2017.E01
```
So we use find (the "inode", or meta-data structure) using -n to find the 2048 offset again in our NTFS file system by running mmls. The return value we get from 285, the MFT entry for Alberte's NTUSER.DAT file.

Alternatively, if you want to search for all NTUSER.DAT files on a system, you could use fls with the option to recursively list all files (-Fr), grepping the output for NTUSER.DAT. In either case, find the MFT entry for Alberte's NTUSER.DAT is: 285:

```
barry@forensic1:-$ fls -Fr -o 2048 NTFS_Part_2017/NTFS_Part_2017.E01 | grep NTUSER.DAT
Users/Alberte/NTUSER.DAT
Once've identified the MFT entry using one of the two methods, you can simply extract the file with icat, arbitrarily naming the output (we use NTUSER.285 here). Run the command to check the resulting type:

```
barry@forensic1:-$ icat -o 2048 NTFS_Part_2017/NTFS_Part_2017.E01 > NTUSER.285
```
Now that we have the registry file we can choose a specific key to search for useful information. As an example, we will look at the UserAssist entries. These entries occur in the registry when a user executes a program from the desktop located at `Software\Microsoft\CurrentVersion\Explorer`. For a complete explanation, refer to the aforementioned book by Harlan Carver. So we have our registry file, NTUSER.DAT, and target key, UserAssist. We need to access the data. For this, install libregf:

```
barry@forensic1:-$ su libregf...
root@forensic1:-# exit
```
You can have a look at the utilities that were installed by looking at the file in `/var/log/packages/libregf-20170130-x86_64`. We can see that three executable programs placed in `/usr/bin`. We will concentrate on using regmount. Like libewf (which is also part of the project), regmount provides a file system interface to a file, in this case. The usage is very similar. First, we will create a mount point in our current directory, followed by the registry:

```
barry@forensic1:-$ mkdir ntusermnt
barry@forensic1:-$ regmount NTUSER.285 ntusermnt
barry@forensic1:-$ cd ntusermnt
barry@forensic1:-/ntusermnt$ ls AppEvents/ Keyboard Layout/ Console/ Environment/ System/ Control Panel/ Identities/
```
The registry file NTUSER.285 is mounted using regmount on the mount point we created, ntusermnt (in the current directory). When we change to the ntusermnt directory, we see the contents of the registry file in the same sort of hierarchical structure as would be found in any other registry. We can navigate and view using normal command line utilities. So us navigate to the UserAsset key and view the contents:

```
barry@forensic1:/ntusermnt$ cd Software/Microsoft/Windows/CurrentVersion/Explorer/UserAsset/
barry@forensic1:/ntusermnt/Software/Microsoft/Windows/CurrentVersion/Explorer/UserAsset$ ls
{CEBFF5CD-ACE2-4F4F-9178-9926F4174EA}/
{F4E57C4B-2036-45F0-A9AB-443BCE3D9F}/
```
You can see once that the directory prompt is quite long! When we run our command, we see two cryptic looking directory (GUID) entries: Directory `{F4E57C4B-2036-45F0-A9AB-443BCE3D9F}` and the directory `Count/values`. Note that when you use the `<values>` sub directory, you will need to escape the parentheses with `\` so you will use `\(values)`.

```
barry@forensic1:/ntusermnt/Software/Microsoft/Windows/CurrentVersion/Explorer/UserAsset$ {F4E57C4B-2036-45F0-A9AB-443BCE3D9F}
barry@forensic1:/ntusermnt/Software/Microsoft/Windows/CurrentVersion/Explorer/UserAsset/(values)/
barry@forensic1:/ntusermnt/Software/Microsoft/Windows/CurrentVersion/Explorer/UserAsset/{F4E57C4B-2036-45F0-A9AB-443BCE3D9F}/Count/(values)
```
Now have a look at the contents of this directory. I am going to abbreviate the command prompt with `...` to make the lines more readable:

```
barry@forensic1:/...Count/(values) $ ls
HRZ_GYRFFVBApage
HRZ_GYPYNHPHag
```
This is where bash completion comes in. Using the `cd` command here, type the first characters and hit `<tab>`... the rest will be automatic.

What's the best way to run the `tr` command on all the files in the `/values` directory? We can go back to the short bash loop we introduced in the Viewing section:

```bash
barry@forensic1:/Count/(values)$ for file in *
do
    echo "$file" | tr 'n-zN-Z' 'a-m-A'
done
```
If you did any reading on this particular, you'll find that the above (or "files" in our mounted system) are obfuscated. This means that the characters in each string are swapped (n-z), so an "a" becomes an "n" and a "b" becomes an "o", and so on. We can deobfuscate this with the `tr` command used previously to replace one character with another. In this case, we'll be repeating the string on each line, yours:

```
barry@forensic1:/Count/(values)$ echo "." | tr 'n-zN-Z' 'a-m-A'
```
We can see that the string at the end of each line is actually the `.lnk` file extension.

```
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Sticky Notes.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Welcome Center.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Calculator.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\displayswitch.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Administrative Tools\Computer Management.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Windows Explorer.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Google Chrome.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Internet Explorer.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Mozilla Firefox.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Magnify.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Fax and Scan.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\XPS Viewer.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Accessories\Paint.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Remote Desktop Connection.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Accessories\Sniping Tool.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Sticky Notes.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Welcome Center.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Calculator.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\displayswitch.lnk
- {013994E-6AFFE-49F2-8690-3AFCAE6FF8}\Administrative Tools\Computer Management.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Windows Explorer.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Google Chrome.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Internet Explorer.lnk
- {92E95A5-19FC-413-8227-48B2BC7174}\Mozilla Firefox.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Magnify.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Fax and Scan.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\XPS Viewer.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Accessories\Paint.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Remote Desktop Connection.lnk
- {A7F7D57-22E8-443C-A6A2-301055A6FF8}\Accessories\Sniping Tool.lnk
```
