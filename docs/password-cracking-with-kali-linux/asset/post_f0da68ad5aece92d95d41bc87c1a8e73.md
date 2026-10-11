
## Prince Processor

It also seems that you can use two separate wordlists with PP, and it seems to take words from both:

```
pp64.exe --pw-min=10 < HugeWordlist.txt SecondWordlist.txt > PrinceHugeSecond.txt
```

The downside is that this creates HUGE wordlist files really fast. Don't let it run for more than a few seconds, unless you have a very large hard drive. You have been warned!

I crack a lot of complex lists for fun, and have had little success with PP. Though taking a PP generated wordlist (PrinceWordlist.txt from above) and then running it in hashcat using hashcat rules has been somewhat successful for me. Lastly, Prince Processor comes with two rules that you can use to further modify words, just like you can in regular hashcat.

See the Prince Processor rules webpage for more information:
https://github.com/hashcat/princeprocessor/tree/master/rules

# PASSWORD CRACKING - PATTERNS

When cracking passwords, always look for patterns in the cracked passwords. Humans are creatures of habit and the familiar, so there are almost always patterns. Once you have the pattern, then you can create custom wordlists using those patterns. For instance, working through a combined public password dump of passwords that other hackers hadn't been able to crack yet, I found character codes in the dump. Instead of using the ampersand, apostrophe, quotation marks, less than, or greater than signs when the database stored the hashes, it turned them into HTML (or XML) character codes and then hashed them. So, instead of storing an "&" in the password database, an "&amp;" was stored. Or, the decimal ASCII code was used, "#038".

Thus, the password "behappy&" became "behappy&amp;". It was then converted into a hash and stored. When cracking these passwords, you have to create a wordlist using the character codes.

I created a custom wordlist using all the character codes I saw in the dump, including:

- &amp;
- &apos;
- &quot;
- &lt;
- &gt;
- &#038;
- &#039;
- &#032;
- &#033;
- &#034;
- &#035;
- &#037;

I used this with my standard wordlists and only found a few. The problem was, the codes were used in the middle of the password, usually to separate two or more words. This is easy to replicate using the Hashcat utilities.

I used the "combinator3" command to take two really short wordlists and I put my custom list in the middle:

```
combinator3 1K_wordlist.txt CustomCodes.txt 1K_wordlist.txt > word_custom_word.txt
```

**WARNING!!** *You have to be very careful using combinator and especially combinator3. They create a wordlist using every possible combination of the input words, so the output will be exponentially larger than the input wordlists alone. They can (and will!) fill a hard drive if you use large lists -- you have been warned!*

This combination cracked a lot of passwords, I knew I was on the right track - But I needed a larger wordlist. Instead of risking combinator3 with a larger list, I just used combinator with my custom wordlist and a 1 million word wordlist.

```
combinator CustomCodes.txt 1M_wordlist.txt > custom_1Mword.txt
```

I could then use this new wordlist and, using a "a1" combinator attack in hashcat, I could use any other wordlist for the beginning and the custom 1 million list for the end.

```
hashcat64 -D 2 --remove -m 0 hashes.txt -o cracked.txt -a1 10MillionWords.txt custom_1Mword.txt
```

Hashcat then took my 10 million wordlist and combined every word in it with my custom code and the 1 Million word wordlist. This cracked a very large number of passwords!

The cracked passwords looked like these:

```
ocean&;river15
toast&;brot
anoud&;hamdan123
mammy&;ffion
vanee&;juan98
```

This is just one example of how in cracking you analyze the cracked passwords that you have, look for patterns, and then, create your own custom wordlists. Then use the custom wordlists combined with other wordlists using hashcat to go for the win!

# USING CRACKED PASSWORDS TO CRACK NEW PASSWORDS

One of the best advanced cracking techniques is to use the passwords that were cracked as a wordlist, and then using them in combo attacks or running rules on them. This is easy to do by parsing the Hashcat cracked output file. The output file will have the original hash, a colon, and then the cracked password. All we need to do is remove the hash and colon, and then re-save the file as a new wordlist.

The Linux text manipulation commands are great for parsing wordlists. In particular the "cut" command. All you need to do is figure out where the hash & colon ends and then cut the passwords out and save them in a new file. In the wordlist example below, the passwords start at column 34.

```
cut -c34-128 cracked.txt > crackedwl.txt
```

```
(kali@kali) - ~/Desktop
head cracked.txt
fc7075dcdcbc2473f123b963e0e6f:5apinbrumeux
4ad5f0f0c5eeacafdf878e89eec460c8:victorieusescals
9c16657819ce138393ca44605c978296:idyllechassures
0d08dc6f3f87515d420031a91bbc8460:jupecloutee
6c731281893238743c43aa0b031dd345:aller courageuse
963a650665e9a52e25fc048432062556:achatsdepenses
14a6e06e9ce76b91d8c25ca06333a3d2:hydratantefficace
138be4dafd1a5485558309d4264ba082:mailleenchaine
3af23e313fb8f1c80f420d29bb6f0421:ornefourrure

(kali@kali) - ~/Desktop
cut -c34-128 cracked.txt > crackedwl.txt

(kali@kali) - ~/Desktop
head crackedwl.txt
sapinbrumeux
victorieusescals
idyllechassures
jupecloutee
aller courageuse
achatsdepenses
hydratantefficace
mailleenchaine
ornefourrure
```

Another helpful technique when creating your own wordlists or combining existing ones is to sort & remove duplicates:

```
sort wordlist.txt | uniq -d > finalwordlist.txt
```

This technique is great when you have combined several wordlists into a new one.

# PACK - PASSWORD ANALYSIS AND CRACKING KIT

Tool Author: Peter Kacherginsky (iphelix)

Tool GitHub: https://github.com/iphelix/pack

Lastly, let's take a quick look at a couple other useful password tools. PACK is a collection of tools for advanced password analysis and cracking. PACK makes it very easy to analyze statistics and create masks and rules.

```
git clone https://github.com/iphelix/pack.git
```

![](img/4a03f08556c51a14a3b88fe549a54ca8_136_0.png)

Analyzing a crackerd wordlist for patterns and statistics:

```
python2 statsgen.py crackerdwl.txt
```

```
[*] Character-set:
[+]               numeric: 68% (338452)
[+]      loweralphanumeric: 10% (50445)
[+]      mixedalphanumeric: 09% (44627)
[+]      loweralpha: 03% (18789)
[+]      all: 02% (14243)
[+]      loweralphaspecialnum: 02% (10292)
[+]      mixedalpha: 01% (5336)
[+]      loweralphaspecial: 00% (4133)
[+]      upperalphanumeric: 00% (2676)
[+]      mixedalphaspecial: 00% (1367)
[+]      upperalpha: 00% (833)
[+]      upperalphaspecialnum: 00% (558)
[+]      specialnum: 00% (552)
[+]      special: 00% (203)
[+]      upperalspecial: 00% (71)
```

You can use the tools from the PACK kit to creating masks from wordlists:

- `statsgen.py crackedwl.txt -o crackedwl.masks`
- `maskgen.py crackedwl.masks --occurrence -q -o crackedwl.hcmask`

(You can also use, "--targettime" to limit cracking times)

```
┌──(kali㏒kali)∼[~/pack]
└─$ python2 maskgen.py crackedwl.masks --occurrence -q -o crackedwl.hcmask
[*] Analyzing masks in [crackedwl.masks]
[*] Saving generated masks to [crackedwl.hcmask]
[*] Using 1,000,000,000 keys/sec for calculations.
[*] Sorting masks by their [occurrence].
[*] Finished generating masks:
Masks generated: 26837
Masks coverage: 100% (492577/492577)
Masks runtime: >1 year
```

You now have a file that contains cracking masks for hashcat:

```
(kali@kali) ~/pack
$ cat crackedL.hcmask
?d?d?d?d?d?d?d?d?d?d?d?d?d?
?d?d?d?d?d?d?d?d?d?d?d?d?d?
?
```

This returns a huge number of masks, and as you can see, the cracking time is greater than a year. We don't have time for that, so let's see if we can fine tune the list. We will use “targettime” to do this.

```
python2 maskgen.py crackedwl.masks --targettime 900 --optindex -q --showmasks
```

This will return a list of optimized masks that should be finished in about 15 minutes. You can then feed this file into hashcat using a regular -a3 mask attack and it will use each mask in the file one after another. Kind of like an automated brute force attack!

```
hashcat -D 2 --remove -m 0 uncracked.txt -o cracked.txt -a3 quickmasks.hcmask -O

Session..........: hashcat
Status...........: Running
Hash.Type........: MD5
Hash.Target......:
Time.Started.....: Sat Jul 17 21:11:04 2021 (2 secs)
Time.Estimated...: Sat Jul 17 21:11:27 2021 (21 secs)
Guess.Mask.......: ?u?d?d?!?d?d?u?d?d [9]
Guess.Queue......: 3/108 (2.78%)
```

Hashcat will run a brute force attack using each mask, one after the other, until it reaches the end of the file. Statistics and masks are a very useful tools to help crack a difficult password hash list. This was just a quick overview of the PACK tools, check out the tool website for a much more in-depth explanation of the tools.
