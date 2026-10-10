
## Level 6 Problem

Login: level6  
Password: Best of The Best  
Study: Port Scan.

This is one of the easiest levels of HackersLab. It's for a really relaxed time. It focuses on the following fact: there is a second open door for access to the system. What are these doors? Whenever you connect to a system, a "Socket" is created. A socket is nothing more than the IP + port combination service door. This allows the same internet address to have multiple services running as Web Server, FTP, SMTP, POP, and others.

Some common port numbers:
- 21 - FTP
- 22 - SSH
- 23 - TELNET
- 25 - SMTP
- 79 - FINGER
- 80 - WWW
- 3128 - PROXY
- 6000 – XWINDOWS

SERVER, common ports using TCP and UDP protocols.

For example: when I connect to any web page like http://www.visualbooks.com.br, I'm actually connecting to http://www.visualbooks.com.br:80 (visualbooks.com.br, on port 80, which is the web standard). So far it seems easy. But we fall into the following problem - there are 65535 ports for both TCP and UDP protocols. There are doors that never end anymore. How can we find out which ones are open and which aren't? By using door scanners. Port scanners are applications that try to find out in a certain IP address or host, which ports are open. They can usually use a list of most known ports, or a range (example: from 1000 to 8000). They are usually extremely fast and results quickly return to us. Common port scanners perform a TCP connect() on the most targeted machine. This means that it performs the three TCP authentication paths (syn-syn/ack-ack). Using this system, it is easy for the scanner to discover the scanning attempt. A firewall or IDS, for example, quickly captures the hacker's IP. To end this, there are now more sophisticated scanners, like NMAP. NMAP, which can scan in many ways besides TCP connect(), has half syn() scanning (only sent syn), fin, Xmas and others. Each type uses different flags to make it difficult to detect the scanned host. At this step-by-step level, I will use two different scanners: NMAP, for Linux, and VALHALLA for Windows and we'll try to find the port.

We connected as level6 and did the basics again. But we don't have any files now ... why? Of course ... I must find a door system access, but do not attempt to break the security of any files. Let's use NMAP first to try to detect the port. After sending NMAP to scan drill.hackerslab.org, it returned me three: 23, 80 and 6969. Now 23 is from telnet, 80 from the webserver and this 6969? Hmmm, very suspicious. Let's move VALHALLA to Windows, then. VALHALLA is a program created by me, which besides a scanner of hosts and IPs, is a monitor of ports and portscan detector. It can be picked up at [http://www.anti-trojans.cjb.net](http://www.anti-trojans.cjb.net). Almost the same result. Found port 23 at 80, 100 and 6969. The most suspicious for sure is 6969. Let's telnet to it and see what happens.

Just enter `telnet drill.hackerslab.org 6969`, placing the port in front of the name. The result came up? A login prompt similar to the usual HackersLab login appeared. Asked for my level6 password ... after typing, bing0! The system returned to me: assets!! Level7's password is **Can't help falling in love**. I already said this level would be easy ... no?

## Level 7 Problem

Login: level7  
Password: Can't help falling in love  
Study: Breaking Unix / Linux Passwords.

Many older hackers are already used to the words DES, shadow, CrackerJack, John the Ripper ... shame the new generation doesn't have such intimacy with these terms. Unix / Linux uses a password encryption system called DES. This system creates an encrypted string and places it in the security file system names which are usually `/etc/passwd`. Used to use now `/etc/shadow`. They moved to the shadow archive hoping to increase the security, leaving the original password with only the usernames. Those who take control of the system can get any file, even the shadow.

A typical shadow entry:
`mflavio: yFdrXa1EwNYng: 12126: 0: 99999: 7 :::`

According to the previous information, we have the username as `mflavio`. Encrypted Password: `yFdrXa1EwNYng`. The rest of the numbers are System IDs (UID, GID, etc.).

Great, I have a user's password on Linux, but it's encrypted! No problem, I'll get a program that decrypts. That sounds feasible, but that's impossible. As I said before, DES creates a hash, which is a one-way encryption system. It cannot be decrypted. But then ... how do we find out the password? Just use your imagination. Think: if the password in shadow cannot be decrypted, how does the system compare this password with the password that the user types when logging in? Easy. The system encrypts the new password and compares the two encrypted values. If they are equal, that is the password.

CrackerJack and John The Ripper are programs that allow you to use a wordlist or brute force to “crack” Unix / Linux. They will encrypt each word using DES and compare it with the password that is in the password file. If the result hits ... that's the right password. Of course, for this, you need to have a good wordlist. A wordlist contains passwords commonly used and divided into categories like movie names, German words, etc ...

Let's see again, in practice, how this process is done.

We log into HackersLab and look for the file with UID level8 and GID level7. We found `/dev/audio2`. We enter the `/dev` directory and run `./audio`. The program shows some trash on the screen. But is it really rubbish? It shows three strings (which could probably also be obtained using this string) command: `level8`, `shadow`, and `VoE4HoQCFfiMWw2`. Well, I deduced a little bit, by the hash face of the last string and the other two, I think we found the password ... encrypted.

We will have to try to find out the password using John the Ripper (which can be obtained at [http://www.blackcode.com](http://www.blackcode.com)). But first, we need to stop the wordlist and adapt the encrypted password. Is there a way you can try to figure out the password just by typing the hash as John the Ripper's command line? For this, you could use a single option. But for study questions, we took a shadow file and replaced the root password with our obtained hash. Thus, we simulated and cracked a shadow file. The JTR (John The Ripper) will try all the words in this list as passwords. The list has been saved as `passwords.txt`. Now, let's use JTR. JTR was executed as `john – wordfile: passwords.txt shadow` (sig-Nice: Dear John, please use the wordlist passwords.txt to remove passwords which will be tested in shadow). It quickly returned the password to me.

It is wonderful. What a strange word is that? Pen-a little while later we find out: `wonderfu` actually is `wonderful` only from English, one of the words on our list. But why did he only show eight characters (the last one is the missing "l")? This is the same problem that occurs when the Program File directory becomes a file. The program is DOS-based, and it can show only eight characters. Of course, you can change that in the rules. To learn more, take a look at the JTR manual. What matters is that the password for level8 is **wonderful**!

## Level 8 Problem

Login: level8  
Password: wonderful  
Study: Race Conditions.

At this point, a lot of changes in the HackersLab challenge. Levels below these were pretty simple so there wasn't much to talk about studying, this change now from race conditions. They are conceived a little more complicated than we dealt with till now and these require a greater knowledge (including code examples) to be properly understood. If you don't know C, it would be better if you had a notion before, but for now, it doesn't matter. Understanding the general concept behind the problem is already a step forward.

This much theoretical introduction of the race condition problem is necessary to understand how it occurs, how problems occur between two reads and write functions and get a sense of which functions can be used to correct a certain problem. If you have no notion of C and were "floating" in the explanation, I suggest you try to learn a little, because all levels after this will use programming. This level was much higher than the previous ones and it will be easy to understand step by step.

We connect to HackersLab as level8, we find the file for level9 UID and level8 GID. We found what was mentioned in the problem, `/usr/bin/ps2`. After entering the `/usr/bin` directory, tried to run `./ps2`. Nothing happens ... but really? We know that it creates a temporary file, but suppose that we were not told about it. So we can “check” our actions using the `strace` command. Typing `strace /usr/bin/ps2` (without the quotation marks). Let's take a look at what the command generated: Sounds like a joke ... there is everything we saw in the study ... the `open()` function opening a temporary file without any descriptor checks, attempting to write the string `hahahahahahaha` using the `write()` function without reading any of the permissions, and worse, giving us the filename instead of creating a random file.

Let's try to create some "little scripts" to link the temporary file `/var/tmp2/ps2.tmp` created by the `ps2` program to some content of our interest. You will have to use the VI text editor to create two small
