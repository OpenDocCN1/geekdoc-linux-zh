# ELEMENTARY CONFIGURATION STEPS 135

# Survival rule 4

There may be several reasons why you do not find a particular configuration file in your distribution, one of which being that the underlying program packages have not been installed at all – therefore, make yourself familiar with the package management of your distribution:

+   - rpm (Caldera, DLD, RedHot, SuSE, and so on): page 213
- gnorpm (RedHat): page 732
- dpkg. (Debian): page 711
- yast (SuSE): page 741

A alternative is even more probable – the file exists, but is stored in a different location. (Directory paths tend to vary not only from distribution to distribution, but with every version!) The following commands will help you with your search:

+   - locate: page 463
- find: page 454
- grep: page 439

This is how you find all files whose name or directory contains grep:

```
root# locate grep
```

The following command shows how you can search /etc and all subdirectories for files whose content (not the file name) contains the word grep:

```
root# cd /etc
root# -find type f -exec grep -q grep \ -print
```

# Survival rule 5

You would be advised to check the online documentation (Chapter 4), as it may be more up-to-date than this chapter!

# 6.2 Elementary configuration steps

This section deals with the most basic configuration problems: correct support of foreign language keyboards, display of foreign language special characters on screen, setting of time system, and so on.

# Keyboard

Many of the problems described in this section emerge from the fact that Unix was developed for American conditions, that for a US keyboard and a 7-bit ASCII character set. Very quickly, the necessity arose to allow for additional characters (the special characters for European countries). And even though there is unanimity about the character set it is called ISO Latin I and bears some resemblance to the ANSI character set used in Windows – there is no conformity at all in how this character set is supported.