
combination with dates and symbols. These are fairly easy to create using the combination techniques I have already covered. Many corporate users currently use this tactic to create their passwords, so I leave this as an optional exercise for the reader to explore. Just remember, using the hashcat combinator tools can create HUGE files fast that WILL fill a hard drive – so watch your hard drive space as the lists are generated and use Ctrl-C to stop the process. You won’t have a complete combined list, but you will have many to play with, and your system won’t crash because your hard drive is full!

For more information, check out the Hashcat Wiki -
https://hashcat.net/wiki/

## CHAPTER 7

### More Advanced Techniques

![](img/4a03f08556c51a14a3b88fe549a54ca8_124_0.png)

Before we leave the topic of Hashcat, let’s look at a few more advanced topics. In this chapter we will take a closer look at Hashcat Rule files. We will see how to bring some automation to Mask attacks with “Mask Files”. Take a look at the Prince Processor attack, a unique way to modify attacks with wordlists. Lastly, we will look at some patterns and tools that could make password cracking easier.

## RULES AND MASK FILES

### Rule based attacks

Mentioned briefly before, rule-based attacks can be very useful. Hashcat has a list of built-in rules that you can use to crack passwords. You can find them in the Hashcat "rules" subdirectory. For example, there are "leetspeak" rule sets that automatically take each dictionary word and try different leet-speak versions of the word, replacing letters with numbers. You can even use a programming type language to create your own rulesets.

```bash
[kali@kali]:/usr/share/hashcat/rules$ ls
best64.rule
combinator.rule
d3ad0ne.rule
dive.rule
generated.rule
generated2.rule
hybrid
Incisive-leetspeak.rule
InsidePro-HashManager.rule
InsidePro-PasswordsPro.rule
leetspeak.rule
oscommerce.rule
rockyou-30000.rule
specific.rule
T0X1C_3_rule.rule
```

Rule based attacks are used in single attack mode. They are enabled by using the `-r` switch and the name of the ruleset you want:

```bash
[kali@kali]:/usr/share/hashcat/rules$ hashcat -m 1000 ~/Hardhash.txt ~/rockyou.txt -r leetspeak.rule -o ~/cracked3.txt
hashcat (v6.2.6) starting

OpenCL API (OpenCL 3.0 PoCL 3.1+debian Linux, None+Asserts, RELOC, SPIR, LLVM 14.0.6,
* Device #1: pthread-sandybridge-Intel(R) Core(TM) i7-6700 CPU @ 3.40GHz, 1435/2935 MB

Minimum password length supported by kernel: 0
Maximum password length supported by kernel: 256

Hashes: 5 digests; 5 unique digests, 1 unique salts
Bitmaps: 16 bits, 65536 entries, 0x0000ffff mask, 262144 bytes, 5/13 rotates
Rules: 17
```

The Best64, InsidePro, Dive, Rockyou-30000 & d3ad0ne rules are some of the more popular ones and are very effective. My best advice for rules is to start with the smaller rule files (look at their file size) and then move on to the larger ones. The smaller ones usually run fairly quick; the larger ones can take significantly longer to run. You can also use multiple dictionaries at once by just listing your dictionary folder instead of listing an individual dictionary file name. Hashcat will then run through every wordlist in the dictionary folder.

You can run several small rules at once by adding multiple `-r` lines to the Hashcat command. This comes in very handy with the "hybrid" rules. Adding two Hybrid rules to an attack will attempt to add letters, numbers, or symbols to both the beginning and end of the wordlist word.

Example:

```bash
hashcat -D 1 -m 1000 Hardhash.txt rockyou.txt -o Hardcracked.txt -r hybrid/append_ldus.rule -r hybrid/prepend_ldus.rule --remove
```

Would take a word from the rockyou wordlist and add a random letter, number or symbol to both sides, as seen below:

```
Guess.Mod........:  Rules (hybrid/append_ldus.rule, hybrid/prepend_ldus.rule)
Guess.Queue......:  1/1 (100.00%)
Speed.Dev.#1.....: 16746.6 kH/s (12.12ms)
Recovered........:  0/3 (0.00%) Digests, 0/1 (0.00%) Salts
Progress.........:  448062273/129448255425 (0.35%)
Rejected.........:  9025/448062273 (0.00%)
Restore.Point....:  49153/14343297 (0.34%)
Candidates.#1....: {tripletX -> ~IlovejT~}
```

The Rockyou word “triplet” was transformed into “{tripletX” and the word, “ilovej” to “~IlovejT~”. You could also add in one of the “Toggles” rules to have it toggle letters in the words to upper or lower case while appending and prepending characters:

```
{TripLetX -> ~IloveJT~
```

Using multiple rules together can greatly expand the cracking ability of simple lists. I have used up to three smaller ones, but by then you start running out of available memory and Hashcat will exit.

### Mask Files

Mask Attacks allow you to define the layout of the brute force words that will be used in your attack. For instance, if you know that the target's password policy requires two numbers, six uppercase letters and two special characters you can create a mask for Hashcat to use.

In this example it would look something like, `?d?d?u?u?u?u?u?u?s?s`:

```bash
hashcat -D 1 -m 1000 Hardhash.txt -o Hardcracked2.txt -a 3 ?d?d?u?u?u?u?u?u?s?s --remove
```

Play around with different masks until you get a feel for how they work. The longer the mask, the exponentially longer it will take for it to run. A three-letter mask could be finished in seconds. A 10+ character mask could take hours or years to run. Hashcat also allows for the use of “mask files” instead of manually providing the mask. Basically, a mask file is just a file that contains multiple masks. Example masks are included with Hashcat, and can be found in the `masks` subdirectory.

Below is a screenshot of the “Rockyou-1-60.hcmask”:

![](img/4a03f08556c51a14a3b88fe549a54ca8_127_0.png)

To use a mask file, you simply provide the mask filename instead of typing a manual mask on the Hashcat command line.

```bash
hashcat -m 1000 Hardhash.txt -o cracked3.txt -a 3 rockyou-1-60.hcmask --remove
```

```
Session..........: hashcat
Status...........: Exhausted
Hash.Mode........: 1000 (NTLM)
Hash.Target......: /home/kali/Hardhash.txt
Time.Started.....: Mon Mar   6 16:20:05 2023
Time.Estimated...: Mon Mar   6 16:20:05 2023
Kernel.Feature...: Pure Kernel
Guess.Mask.......: 2l2l2l2l?d [5l]
```

When run, Hashcat will step through the file using each mask listed one by one. As mentioned before, the longer the mask, the longer it will take to run. That is why it is always best to use a video card GPU on a stand-alone system (non-VM) to speed things up, if you have a compatible card. You would change to the GPU using the "-D" switch and you could also use the "-O" switch at the end which will not crack extremely long passwords, but greatly increases cracking speed.

## PRINCE PROCESSOR ATTACK

- Tool GitHub: [https://github.com/hashcat/princeprocessor](https://github.com/hashcat/princeprocessor)
- Releases: [https://github.com/hashcat/princeprocessor/releases](https://github.com/hashcat/princeprocessor/releases)

Prince Processor (PP) is an advanced wordlist combinator attack. It can perform complex wordlist attacks using a single wordlist file. First, set a minimum password length, then provide a wordlist to use. PP will then take the length you provided and begin to build words of that length from multiple words in the existing file. So, if you set a word length of 6, it can take all 6 letters from one word, or it can take 1 letter from 6 words, or 2 letters from 3 words, and any combination in between.

PP then takes these new words and pipes them into hashcat, live on the fly. Hashcat uses the words as a regular wordlist and uses them to crack away. It's not amazingly fast, but if you run out of other options, it is an interesting technique to use. Prince Processor is available for Linux, Windows and Mac.

Here is an example on Windows:

```
pp64.exe --pw-min=12 < HugeWordlist.txt | hashcat64 -D 2 --remove -m 0 uncracked.txt -o cracked.txt -O
```

I’ve had mixed results with Prince Processor, what it does is very impressive, but there is a huge speed hit. That’s why I run it on my Windows gaming system. Though the size of the wordlists doesn’t seem to really affect speed. Prince Processor, on its own is extremely fast, I think the bottleneck is more in piping the output into Hashcat. Though I did find feeding a wordlist into Prince Processor, then outputting it directly to a text file, then using that as a regular wordlist works much faster.
