```
kali@kali:~$ searchsploit "Sync Breeze Enterprise 10.0.28"

| Exploit Title | Path (/usr/share/exploitdb/)
| Sync Breeze Enterprise 10.0.28 - Remote Buffer Over | exploits/windows/remote/42928.py
| Sync Breeze Enterprise 10.0.28 - Remote Buffer Over | exploits/windows/dos/42341.c

Listing 426 · Searching for available exploits for our vulnerable software using searchsploit
```

Since we’re already familiar with how the vulnerability works and how it is exploited, we are presented with a good opportunity to see the differences between scripting languages such as Python and a compiled language such as C without the added complexity of unraveling a new vulnerability.

While there are plenty of differences between the two languages, we will focus on two main differences that will affect us, including memory management and string operations.

The first key difference is that scripting languages are executed through an interpreter and not compiled to create a stand-alone executable. Because scripting languages require an interpreter, this means that we can not run a Python script in an environment where Python is not installed. This could limit us in the field, especially if we need a stand-alone exploit (like a local privilege escalation) that must run in an environment that doesn’t have Python pre-installed.

> As an alternative, we could consider using PyInstaller (https://www.pyinstaller.org), which packages Python applications into stand-alone executables for various target operating systems. However, given the nuances of exploit code, we suggest porting the code by hand to fully understand how the exploit will work against the target.

An additional difference between the two languages is that in a scripting language like Python, concatenating a string is very easy and usually takes the form of an addition between two strings:

```
kali@kali:~$ python
>>> string1 = "This is"
>>> string2 = " a test"
>>> string3 = string1 + string2
>>> print string3
This is a test

Listing 427 · String concatenation example in Python
```

As discussed later in this module, concatenating strings in this way is not allowed in a programming language such as C.

To begin the process of modifying our exploit, we will move the target exploit³⁸⁰ to our current working directory by using SearchSploit’s handy -m mirror (copy) option:

³⁸⁰ (Offensive Security, 2017). https://www.exploit-db.com/exploits/42341/