# v4.33
A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

This exercise still simplifies that of, but it also serves to make you aware of some of the more complex issues that may arise when searching larger images with more complex content. It will also introduce you to some basic application file viewers beyond those we've already seen. The scenario here is the same as previous exercises. We'll pick a keyword, search the entire disk, and then recover and view the associated file. It will be very similar to the EXT exercises we did earlier (2A and 2B). This time, NTFS is our target file system.

Once again, we are dealing with the NTFS_Pract_2017.E01 image set. And, again, since we are doing a physical search using non-EWF aware tools, we'll ewmount the images and work on the raw mounted disk image. This will create a point in our current directory and use ewmount with our normal user account...no need for loop devices and root permissions.

```
$barry@forensic1:~/NTFS_Pract_2017$ mkdir ewmnt
```

```
$barry@forensic1:~/NTFS_Pract_2017$ ewmount NTFS_Pract_2017.E01 ewmnt/
ewfmount 20140608
```

The grep command points to the mounted image in ewmnt/. Since ewmnt is in our current directory (we just created it), there is no need for a leading /.

```
$barry@forensic1:~/NTFS_Pract_2017$ grep -abi cyberbullying ewmnt/ewf1
C€€€($) |€#($) |€€#@Ba>B #ULTIMATEJOURNEYDK.wmv##($) |€#@Ba>B
#ULTIMATEJOURNEYDK.wmv##L€€€€$ |€#(@($) |€#($) |€#@Ba>B
#ULTIMATEJOURNEYDK.wmv##YYYYYY€€$?#<€€???€#:##
9€€€€€€€€€€€€€€€€€€€€€€€€€
```

```
D€€
Dq€€€
```

Cyberbullying by proxy is when a cyberbully gets someone else to do their dirty...

When we execute our search, we are greeted with a significant number of non-ASCII characters that seriously impede the readability of the output. When you scroll down the output, you can see the string we are looking for, but the offsets are obscured.

Back in our basics session, early in this document, we discussed the tr command to translate "control characters" to newlines. This will have the effect of removing the unreadable content from our view as well as from the grep search, which the one for character replacement causes no issue for offset cases. Use tr here:

252