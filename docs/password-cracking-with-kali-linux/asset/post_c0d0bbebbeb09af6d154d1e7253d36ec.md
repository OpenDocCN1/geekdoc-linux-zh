
## WORDLISTS FOR DIRECTORY PATH OR SERVER BRUTE FORCING

Of course, password cracking isn't the only use for wordlists. Many security tools use wordlists for web or directory path enumeration. These tools aren't cracking passwords, but use wordlists to automatically search for directories or files on servers. These lists contain things like common control panel & configuration file names and webserver data paths.

- https://github.com/danielmiessler/SecLists
- https://gist.github.com/jhaddix
- https://wordlists.assetnote.io/

When you download wordlists, there are usually a lot of words that are duplicates or the wordlist can contain a lot of useless information. The following is a tool to clean up wordlists from useless or random junk:

- https://github.com/BonJarber/SecUtils - Clean Wordlist (I do disagree with classifying some symbols as “Noise” words though)

## WORDLISTS INCLUDED WITH KALI

Kali comes with several wordlists that you can use; the problem is just finding them. Most are in the directory of the main program that uses them. On the newer releases of Kali, shortcut links to the other wordlists are stored in the "/usr/share/wordlists" directory. You can also use the Kali Linux menu selection "05 - password Attacks > Wordlists" as a shortcut to this directory.

```
(kali@kali)~$ wordlists
> wordlists ~ Contains the rockyou wordlist
/usr/share/wordlists
|--dirb
|~~dirbuster
|~~fasttrack.txt
|~~fern-wifi
|~~metasploit
|~~nmap.lst
|~~rockyou.txt.gz
|--wfuzz
```

### Rock You Wordlist

One of the most popular wordlists used in cracking is the, "Rock You" wordlist. This is a large collection of millions of passwords that were actually used and pulled from a database dump.

The file is located in the Kali Linux "/usr/share/wordlists/" directory as seen below:

```
(kali@kali)-[/usr/share/wordlists]$ ls
dirb        fasttrack.txt    metasploit     rockyou.txt.gz
dirbuster    fern-wifi        nmap.lst       wfuzz
```

If you notice, the Rockyou wordlist is zipped, the latest version of Kali offers to unzip it for you, or you can do it manually:

```
(kali@kali)~/usr/share/wordlists $
$ sudo gunzip rockyou.txt.gz
[sudo] password for kali:

(kali@kali)~/usr/share/wordlists $
$ ls
dirb		fstrack.txt	metasploit	rockyou.txt
dirbuster	fern-wifi	nmap.lst	wfuzz
```

You can use the "cat" command to view the file if you want, but it is pretty large for terminal viewing.

## JOHN THE RIPPER Wordlist

The ever-popular password cracker John the Ripper comes with a somewhat smallish password list, but it does include many of the most popular passwords used on the web.

- The file is located in the `/usr/share/john/` directory, as seen below:

```
(kali@kali)~/usr/share/john $
$ ls *.lst
password.lst
```

## WFUZZ Wordlists

Wfuzz is a website brute force attack tool. Though all the wordlists may not be helpful, some are interesting, especially the ones in the “general” directory.

- The files are located in the `/usr/share/wfuzz/wordlist` directory as seen below:

```
(kali@kali)~/usr/share/wfuzz/wordlist $
$ ls
general	Injections	others	stress	vulns	webservices
```

## Additional Wordlists

As I mentioned earlier, there are several other programs with wordlists in the `/usr/share/` directory. Though “RockYou.txt” is probably one of the best built-in ones. If you want to try additional wordlists, just poke around the `/usr/share/` directory and see what you can find.

## WORDLIST GENERATOR TOOLS

Downloading existing wordlists is not your only option. Several tools in Kali let you make your own personalized wordlists. CeWL is pretty useful as it lets you create passwords by grabbing information from a target website. Crunch is nice too as it allows you to create your own custom wordlists from scratch. Let's take a closer look at how to use these tools.

# CEWL

**Tool Author**: Robin Wood

**Tool Website**: https://digi.ninja/projects/cewl.php

![](img/4a03f08556c51a14a3b88fe549a54ca8_56_0.png)

CeWL is a great tool for creating company related or theme-based wordlists. Many times, a user will create a password using words that relate to where they work or what they do. CeWL crawls a target website and builds a custom wordlist file using words found on the site.

- CeWL is no longer installed by default, but just type `cewl` to install.

To use CeWL, provide the options that you want and the target URL. For example, if we wanted to spider the website, "cyberarms.wordpress.com", to a depth of 1 layer (-d 1) pull any words six characters or longer (-m 6) and save it as "cyberarms.txt", we would use the following command:

```bash
cewl -w cyberarms.txt -d 1 -m 6 https://cyberarms.wordpress.com/
```

```
(kali@kali)-[~]~~
$ cewl -w cyberarms.txt -d 1 -m 6 https://cyberarms.wordpress.com/
CeWL 5.4.8 (Inclusion) Robin Wood (robin@digil ninja) (https://digi.ni
(kali@kali)-[~]~~
$ cat cyberarms.txt
Security
Computer
content
January
December
October
February
September
August
release
Cybersecurity
```

CeWL crawls the target website and creates a wordlist with the terms that meet our criteria. The resultant text file might need to be cleaned up a bit before use, but this is a very useful tool.

# CRUNCH

**Tool Authors:** Mimayin, Bofh28

**Tool Website:** [https://sourceforge.net/projects/crunch-wordlist/](https://sourceforge.net/projects/crunch-wordlist/)

Crunch is a great program that allows you to create your own custom password lists. Simple tell crunch what you want, the length and complexity, and Crunch makes it for you.

```
(kali@kali)-[~]
$ crunch -h
crunch version 3.6

Crunch can create a wordlist based on criteria you specify.
The output from crunch can be sent to the screen, file, or
to another program.

Usage: crunch <min> <max> [options]
where min and max are numbers

Please refer to the man page for instructions and examples on how to use crunch.
```

The Crunch manual page (in a Kali terminal, enter `man crunch`) contains complete instructions and examples on how to use the tool. Basically, all we need to tell crunch is the minimum and maximum length of the words, what type of characters to use, and Crunch does the rest. Crunch makes heavy use of the *charset.lst* file that is located in its install directory - “/etc/share/crunch”. So, you will need to either run crunch from that directory or point to the directory with the “-f” switch when using the more advanced character sets (shown below).

Alright, let’s start with an easy one:

> At a terminal prompt, type, `crunch 1 3 -o threeletters.txt`

This tells crunch to start with a single letter (**1**) and finish with three (**3**), it then saves the output (**-O**) as “threeletters.txt”. Basically, crunch starts out with a single letter “a” and cycles through all permutations until it gets to “zzz”.

Will produce something like this:

- a, b, c, d, e, f, g, h, i, j, etc...
- aa, ab, ac, ad, ae, af, ag, ah, ai, aj, etc...
- aaa, aab, aac, aad, aae, aaf, aag, aah, aai, aaj, etc...

If we play around with the options, we can create more complex lists.

- Enter, “crunch 3 4 abcde1234 -o alphanumeric.txt” as seen below:

![](img/4a03f08556c51a14a3b88fe549a54ca8_59_0.png)

This command creates a wordlist that starts with 3 characters (aaa) and ends with four (4444) using alpha/ numeric combinations using ‘abcde1234’. This produces a text file with strings like:

- aa1, bb3, ec4, 2a21, and e3da

# CRUNCH - USING THE CHARSET.LST FILE

Crunch’s Charset.lst file contains a list of keywords that are pre-defined as alphanumeric or symbol strings. We can use these keywords so we don’t have to manually type in the characters that we want to use. The file is located in the `/usr/share/crunch` directory. If we view the file, we can see what keyword sets are available:

- ➤ `cd /usr/share/crunch` 
- ➤ `cat charset.lst`

![](img/4a03f08556c51a14a3b88fe549a54ca8_60_0.png)

We can use any of the defined sets, for example:

- ➤ `sudo crunch 2 4 -f charset.lst mixalpha-numeric-all -o mixedall.txt`
