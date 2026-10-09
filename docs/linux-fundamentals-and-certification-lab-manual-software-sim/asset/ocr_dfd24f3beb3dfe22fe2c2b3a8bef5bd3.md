# Listing a tar File

Often the name of a tar file is cryptic and does not indicate what is in the file. Listing the contents of a file indicates what is in the file and where it will be placed when the file is un-tarred. The syntax is **tar -tvf tar_filename.tar**, where tar_filename.tar is the tar file to be listed. For example, to list the contents of the tar file adom_11-01-2003.tar (Figure 6–2), use the **tar -tvf adom_11-01-2003.tar** command:

![](bbox=[0.05, 0.35, 0.27, 0.395])

```
[jsmith@Styx jsmith]$ ls -l
total 2640
drwxr-xr-x 2 jsmith jsmith 4096 Aug 6 2001 adcom
-rw-r--r-- 1 jsmith jsmith 2693120 Oct 1 10:11 adcom_11-01-2003.tar
[jsmith@Styx jsmith]$ tar -xvf adcom_11-01-2003.tar
-rw-r--r-- jsmith/jsmith 78790 2001-08-06 14:09:08 home/jsmith/adcom/adcom/
drwxr-xr-x jsmith/jsmith 0 2001-08-06 14:09:08 home/jsmith/adcom/
-rw-r-xr-x jsmith/jsmith 2398548 2001-08-06 14:09:08 home/jsmith/adcom/adcom
-rw-rw-r-- jsmith/jsmith 175938 2001-08-06 14:09:08 home/jsmith/adcom/manual.doc
-rw-rw-r-- jsmith/jsmith 58670 2001-08-06 14:09:08 home/jsmith/adcom/readme.lst
-r--r-- jsmith/jsmith 57804 2001-08-06 14:09:08 home/jsmith/adcom/adcomfaq.txt
[jsmith@Styx jsmith]$
```

# Extracting a tar File

Extracting files from a tar archive is one of the most common tasks of a Linux administrator. Files that are transmitted over a network are commonly tarred to make administration easier. The syntax is **tar -xvf tar_filename.tar**, where tar_filename.tar is the name of the tar to extract. For example, to extract the contents of the tar file adom_11-01-2003.tar into the current directory (Figure 6–3), use the **tar -xvf adom_11-01-2003.tar** command:

![](bbox=[0.05, 0.71, 0.27, 0.76])

```
[jsmith@Styx jsmith]$ ls -l
total 2636
-rw-rw-r-- 1 jsmith jsmith 2693120 Oct 1 11:19 adcom_11-01-2003.tar
[jsmith@Styx jsmith]$ tar -xvf adcom_11-01-2003.tar
adcom/
adcom/adcom
adcom/manual.doc
adcom/readme.lst
adcom/adcomfaq.txt
[jsmith@Styx jsmith]$ ls -l
total 2640
drwxr-xr-x 2 jsmith jsmith 4096 Aug 6 2001 adcom
-rw-rw-r-- 1 jsmith jsmith 2693120 Oct 1 11:19 adcom_11-01-2003.tar
adcom adcomfaq.txt manual.doc readme.lst
[jsmith@Styx jsmith]$
```