
The **combinator3** command is similar to **combinator**, but it focuses on generating more complex wordlist combinations by combining three input files. This can be especially useful for creating hybrid wordlists with increased variation.

Basic usage:

```
combinator3 [OPTIONS] [INPUT_FILES] > [OUTPUT_FILE]
```

For instance, to combine three wordlists, **dictionary1.txt**, **dictionary2.txt**, and **dictionary3.txt**, you would run:

```
combinator3 dictionary1.txt dictionary2.txt dictionary3.txt > combined_wordlist.txt
```

> **WARNING:** *Combinator creates massive output files, Combinator3 generates even LARGER files! I always watch my hard drive free space and hit "CTRL-C" to stop the generation if the files get too large.*

Depending on your specific needs, you can further customize the generated wordlists using Hashcat Utils' commands. For example, you can remove duplicates, sort the lists, apply rules, or use other utilities to refine your wordlist before using it with Hashcat for password cracking.

See the tool Wiki page for more information:

[https://hashcat.net/wiki/doku.php?id=hashcat_utils](https://hashcat.net/wiki/doku.php?id=hashcat_utils)

# HASHCAT KEYMAP WALKING PASSWORD WORLDSLISTS

Hashcat’s keymap walking tool, “KwProcessor”, quickly and easily generates password lists based on keymap walking techniques. Many users use keymap walk style passwords. In this section, we will take a quick look at how to use this tool.

## INTRODUCTION

Keymap walking passwords are popular amongst many organizations, especially government entities. They are pretty easy to use and remember. Basically, you start with a specific key on the keyboard and then pick a direction (or multiple directions) and start hitting keys. Your password is entered as you “walk” across the keyboard.

You can create a complex password in this manner by using the shift key and including numbers in the pattern, as seen below:

![](img/4a03f08556c51a14a3b88fe549a54ca8_72_0.png)

Starting with the letter “z”, we move North West, hitting the “a”, “q”, and “1” keys. We then move East a row, hitting the number “2”, and then move South East back down the keyboard hitting the “w” key and stopping on “s”. This would create the password, “zaq12ws”. If we alternately used the shift key, we would get the password, “ZaQ1@WS” which is a little more complex.

What makes keymap walking so successful (until now) is that an attacker would need to know the starting key, direction, direction changes, if any special key is used and when, and of course the ending key. Hashcat's KwProcessor tool makes creating keymap walking wordlists very easy to do.

## INSTALLING KWPROCESSOR (KWP)

Like the Hashcat utils, kwp is an optional download from hashcat. Just download the latest release or you can make it from source. Downloading the latest release is the best option as it hasn't been updated in a few years.

- Download the latest release - [https://github.com/hashcat/kwprocessor/releases](https://github.com/hashcat/kwprocessor/releases)
- Extract the file
- Use "`./kwp`" to run the program

## KEYMAPS AND ROUTES

To crack keymap walking passwords you will need two things, a layout of the keyboard keys and a list of routes to take to create the wordlists. In the kwp program directory you will find the *“keymaps”* and *“routes”* folders:

```
(kali@kali):~/kwprocessor $ ls
basechars  doc  keymaps  kwp  kwp32.exe  kwp64.exe  routes
```

The Keymaps folder contains the keyboard layout for multiple languages:

```
(kali@kali):~/kwprocessor/keymaps $ ls
de.keymap en.keymap es.keymap fr.keymap ru.keymap
(kali@kali):~/kwprocessor/keymaps $ cat en.keymap
1234567890-
qwer tyuiop[]\
asdfghjkl;'
zxcvbnm,./
~!@#$%^&*() +
QWERTYUIOP{}]
ASDFGHJKL:"\
ZXCVBNM<>?
```

The routes folder has 7 preconfigured keymap walks or routes that can be used to generate passwords:

```
(kali@kali):~/kwprocessor/routes $ ls
2-to-10-max-2-direction-changes-combinator.route
2-to-10-max-3-direction-changes.route
2-to-16-max-3-direction-changes.route
2-to-16-max-4-direction-changes.route
2-to-32-max-5-direction-changes.route
2-to-4-exhaustive-prince.route
4-to-4-exhaustive.route
```

We can use these preconfigured routes or create our own using command line switches.

Type, *“./kwp --help”* to see the available options:

```
[kali@kali :~/kwprocessor]_
$ ./kwp --help
Advanced keyboard-walk generator with configurable basechars, keymap

Usage: ./kwp [options]... basechars-file keymap-file routes-file

Options Short / Long                | Type  | Description
====================================+=======+================================
-V, --version                       |       | Print version
-h, --help                          |       | Print help
-O, --output-file                   | FILE  | Output-file
-b, --keyboard-basic                | BOOL  | Include characters reachable wit
-S, --keyboard-shift                | BOOL  | Include characters reachable by
-a, --keyboard-altgr                | BOOL  | Include characters reachable by
-Z, --keyboard-all                  |       | Shortcut to enable all --keyboar
-1, --keywalk-south-west            | BOOL  | Include routes heading diagonale
```

## CREATING A KWP WORDLIST

To create a simple kwp wordlist, we will use the English keymap and the “2-10 max 3 directional changes” route file, as seen below:

```
$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-10-max-3-directional-changes.route
```

This causes kwp to create multiple keymap walk combinations, of 2- 11 characters with a maximum of 3 direction changes:

```
bvbnm,..;p0
cxcvbnm,ki8
vcvbnm,.lo9
xzcvcbnm]u7
-[poiuytrf
@poiuytred
8iuytrewqa
9oiuytrews
=][poiuytg
i';lkjhgf v
ikjhgfdsaz
olkjhgfd sx
p;lkjhgf dc
```

The output of the command is sent directly to the screen, so to create an output file you would need to output the command to a text file:

```
$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-10-max-3-directional-changes.route > basic kwp.txt
```

You can then use the resultant text file as a wordlist in Hashcat.
To create a more complex wordlist, use one of the larger route files:

```
$ ./kwp basechars/full.base keymaps/en.keymap routes/2-to-16-max-3-directional-changes.route > largekwp.txt
```

```
qwertyuiop[|pop| 
-=0987654321qazaq
1234567890-=098i 
'1234567890-0987u 
qwertyuiop[|poik 
-0987654321 1234r
-=09876543212345t 
]|poiuytrewqwertg
-0987654321 12343 
-=098765432123454 
]|poiuytrewqwertr
1234567890-=0989
```

## FOREIGN LANGUAGE KEYWALKS

If you need to crack foreign language keywalks, just use one of the foreign languages keymap files.
So, to create a Russian keywalk wordlist:

```
./kwp basechars/full.base keymaps/ru.keymap routes/2-to-16-max-3-direction-changes.route > rukwp.txt
```

And the resultant file:

![](img/4a03f08556c51a14a3b88fe549a54ca8_79_0.png)

If we have a password hash list that contains any of the words that were generated, it will crack them.
The Hashcat KWP tool is great for quickly create keymap walking wordlists. It’s easy too to change the keymap language, which can come in handy if you are cracking international passwords. If you want to learn more about KWP, check out the Hashcat GitHub page - https://github.com/hashcat/kwprocessor

# WORDLIST WRAP-UP

In this chapter we covered wordlists, how to find them, or how to create your own. Wordlists are a major part of password cracking so it is good to master using them. Most modern passwords that you will run into are normally a combination of a name, numbers and symbol(s). I heavily use the Ignis lists when cracking passwords. I use the Hashcat Combinator tool to combine the smaller Ignis lists.
The other wordlists I use extensively are the Facebook First and Last name lists. These are wordlists of usernames from a Facebook dump. Both of these are rather large for using the Combinator tool with, but combining them with the smaller Ignis lists or with a numbers lists is also highly effective.

Before we move on to using our wordlists with cracking tools to crack hashes, it's important to understand what a hash is and what different types of hashes exist. We will cover this in the next chapter!
