
v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

Also, if we don't know that there are two spaces between Nov and 4, we can tell grep to look for any number of spaces between the two:

```
barry@forensic1:/Logs$ tac messages* | grep ^"Nov[ ]4*"
Nov 4 17:41:27 hostname123 sshd[27630]: session closed for user root
Nov 4 17:41:27 hostname123 sshd[27630]: Received disconnect from 1xx.183.221.214:
11: Disconnect requested by Windows Client.
```

The bold grep translates to "Lines (^) with starting the Nov followed by zero or more (*) of the preceding characters that are between the brackets ([ ] - in this case, a space) followed by a 4". Obviously, this is a complex issue. Knowing how to use regular expression will give you huge flexibility in sorting and organizing large sets of data. As mentioned earlier, read the grep page for a good primer on regular expressions.

Perhaps we need to gather all the entries that we are containing the String Did not receive identification string from <IP> for further analysis.

```
barry@forensic1:/Logs$ tac messages* | grep "identification string"
Nov 22 23:48:47 hostname123 sshd[19380]: Did not receive identification string from 19xx.xx.220.35
Nov 22 23:48:47 hostname123 sshd[19379]: Did not receive identification string from 19xx.xx.220.35
Nov 20 14:13:11 hostname123 sshd[29854]: Did not receive identification string from 200.xx.114.131
```

How many of these entries are there?

```
barry@forensic1:/Logs$ tac messages* | grep "identification string" | wc -l
35
```

There are 35 such entries. Now we just want the data (fields 1 and 2), the time (field 3) and the remote IP address that generated the log entry. The IP address is the last field. Rather count each line in the entry to get the field number of the IP we can simply use the variable $NF, which means "number of fields". Since the IP is the last field, the field number is equal to the number of fields:

```
barry@forensic1:/Logs$ tac messages* | grep "identification string" | awk '{print $1 "$2" "$3" "$NF"}'
```

v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

We can add some \t in place of spaces in our output to make it more readable (this assumes fixed length). The following command will place a tab character between the date and the time, and between the hostname and the IP: (Wait, let's re-examine the flow).

v.4.33 A Comprehensive Beginner's Guide to Linux as a Digital Forensic Platform

## Data Carving with DD

In this example, we will use dd to carve a JPEG file from a chunk of raw data. By itself, this is not a useful exercise. There are lots of tools out that will carve from images, including simple cut and paste from a hex editor. However, the purpose of this exercise is to help you become familiar with dd. First you will need to download the raw data and check its hash:

```
barry@forensic1:/Logs$ wget http://www.linux.org/Files/image_carve_2017.raw
barry@forensic1:/Logs$ sha1sum image_carve_2017.raw
```

It's really a full just of random characters. Wherever there is a standard JPEG image, let's go through the steps we need to recover the picture file using dd and other Linux tools. We are going to stick with command tools available in most default installations.

First we need a plan. How would we go about recovering the file? What are the things we need to know to get the image (picture) out tell dd to start cutting, and how much to cut. The output file will be our JPEG image. Easy, right? So here's our plan, and the tools we'll use:

- 1) Find the start of the JPEG (xxd and grep)
- 2) Find the end of the JPEG (xxd and grep)
- 3) Calculate the start of the JPEG (in bytes using bc)
- 4) Cut from the start to the end and output to a file (using dd)

This exercise starts with the assumption that we are familiar with standard file headers. The end of the JPEG is marked by ffd9. Let's go ahead with step 1: Using xxd, pipe the output of image_carve.raw to less for a brief look:

```
barry@forensic1:/Logs$ xxd image_carve_2017.raw | less
0000000: f0d5 0291 431d 41b4 5f89 5fb9 7240 7543
0000010: 9a71 389a 02e1 04cf 7bbf 32e2 6f99 1133
0000020: fc36 36 dda eb48 56c1 1501 bcfd 2631
0000030: ffa6 3cd3 be3c 77fd d0d4 e9b6 22f2 719b 1a49
0000040: ee92 a2a1 56c2 e2zd 5095 40f4 a234 1208
0000050: da3d 0a2c 9a1c e2dd 5095 40fd a234 1280
0000060: a76d 997e 9d4f 4f9a 9218 a2e1 6d84 1280
0000070: c7df2 5055 12f5 70d3 44b8 8db8 88ed adab
0000080: 9023 e5f4 f4b4 77f5 7c9e 80c3 778 7c1a
0000090: 42c7 9f07 902e 80c9 77f6 67e3 79b8 70f4
0000100: 187a 61f3 3a8c 3096 9d62 e4b8 7504 7e68
```

The end of the JPEG is marked by ffd9. Let's go ahead with step 1: Using xxd, pipe the output of image_carve.raw to less for a brief look. The start of the JPEG header is actually at D8FF. We know that the JPEG begins with D8FF. 

```
barry@forensic1:/Logs$ xxd image_carve_2017.raw | grep "D8FF"
0000000: f0d5 0291 431d 41b4 5f89 5fb9 7240 7543
```
Wait, the previous output didn't show D8FF. Let's look at the file again. 

```
barry@forensic1:/Logs$ xxd image_carve_2017.raw | head -n 20
```
Actually, let's just find the offset of D8FF:

```
barry@forensic1:/Logs$ xxd image_carve_2017.raw | grep -b 1 "D8FF"
```

Once we have the start offset, we can use dd to extract the data. For example:

```bash
barry@forensic1:/Logs$ dd if=image_carve_2017.raw skip=OFFSET bs=1 count=LENGTH of=forensic.jpg
```

After creating the file `forensic.jpg`, we can check if it is a valid image using:

```bash
file forensic.jpg
```

If it's a valid JPEG, we have successfully carved the file. If it's not, we need to adjust the offset and length and try again. This is the basic process of data carving in digital forensics. In a real scenario, you would use automated tools to do this, but understanding the manual process is crucial for verifying what the tools are doing.
