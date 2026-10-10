# **WORK WITH TEXT FILES (SEE CHAPTER 8)**

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Compare two sorted files and view the differences between them with surrounding context? | `diff` | `diff -c first-draft.txt second-draft.txt` |
| Number the lines in a text file? | `nl` | `nl magic.txt > magic-numbered.txt` |
| Convert a Portable Document Format (PDF) file to PostScript? | `pdf2ps` | `pdf2ps resume.pdf resume.ps` |
| Translate all the uppercase characters in a text file to lowercase? | `tr` | `cat uppercase.txt \| tr '[A-Z]' '[a-z]'` |

# **WORK WITH SOUND AND GRAPHIC FILES (SEE CHAPTER 9)**

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Create a thumbnail index of all the graphic files in the working directory? | `convert` | `convert 'vids:*.jpg' catalog.jpg` |
| Create a printed jewel case label for a CD-ROM that I've just burned? | `cdlabelgen` | `cdlabelgen -c 'My Favorites' -s '2000' -i 'BluesJazzRock& Alternative Rock\nTechno\nIndustrial' -e images/mp3.eps > cover.ps` |
| Create a composite image of two or more graphic files using special effects? | `combine` | `combine -compose bumpmap image1.jpg image2.jpg combined.jpg` |

# **CONFIGURE AND USE NETWORKS AND THE INTERNET (SEE CHAPTER 13)**

| How Do I | Use This Command | Example |
| :--- | :--- | :--- |
| Display information about all the TCP/IP sockets currently in operation? | `netstat` | `netstat -a` |
| Copy a file to a remote server for which I have appropriate permissions? | `rcp` | `rcp essay1.doc essay1.bak@lothlorien:/home/suzanne/Documents/Backup` |
| View available NFS shares? | `showmount` | `showmount -a` |
| Mount a Samba share on a remote system? | `smbmount` | `smbmount //lothlorien/suzanne /home/suzanne/lothlorien` |
| Connect to a remote Telnet service? | `telnet` | `telnet lothlorien.mynetwork.org` |