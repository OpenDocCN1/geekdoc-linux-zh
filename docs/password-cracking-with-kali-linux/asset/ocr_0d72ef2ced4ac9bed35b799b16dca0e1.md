+   1. Open a terminal prompt, in the Kali Home directory type, `“hashcat -D 1 -m 1000 Easyhash.txt rockyou.txt -o cracked.txt”`

The “`-D 1`” switch tells Hashcat to use the CPU, normally you would want to use “`-D 2`” to make Hashcat use the GPU, but we are in a Virtual Machine environment. The “`-m 1000`” switch tells Hashcat that our hashes are NTLM based hashes. “`Easyhash.txt`” is the name of our hash file, “`rockyou.txt`” is the name of our dictionary file and “`-o cracked.txt`” tells Hashcat where to store the cracked hashes.

So basically, we provided the hash style, the hash filename, the dictionary file and the output file. The attack options will change, but for the most part this is the basic format that is used consistently with Hashcat.

+   2. Hashcat will then begin to crack the passwords and display a status screen.

As seen in the following image:

![](bbox=[0.17, 0.54, 0.83, 0.85])

+   3. When done, type “`cat cracked.txt`” to see the cracked hashes: