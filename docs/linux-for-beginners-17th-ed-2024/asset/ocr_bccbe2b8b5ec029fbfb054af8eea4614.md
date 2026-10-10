# # Linux Tips and Tricks

As you've seen, the Linux Terminal is quite an exceptional environment. With a few extra apps installed, and a smidgen of command knowledge, incredible, and often quite strange, things can be accomplished.

# ## TAKING COMMAND

There are countless Linux tips, secrets, hacks and tricks out there. Some are very old, originating from Linux's Unix heritage, while others are recent additions to Linux lore. Here's our favourite ten tips and tricks.

# ### EASTER EGGS

Emacs, the text editor, is a great piece of software; however, did you know it also contains a hidden Easter Egg? With Emacs installed (`sudo apt-get install emacs25`), drop to a Terminal session and enter:

```
```bash
emacs --batch -l dunnet
```
```

Dunnet is a text adventure written by Ron Schell in 1982, and hidden in Emacs since 1994.

![](bbox=[0.07, 0.58, 0.48, 0.68])

# ### TERMINAL BROWSING

Ever fancied being able to browse the Internet from the Terminal? While not particularly useful, it is quite a fascinating thing to behold. To do so, enter:

```
```bash
sudo apt-get install elinks elinks
```
```

Enter the website you want to visit.

![](bbox=[0.52, 0.58, 0.93, 0.68])

# ### MOON BUGGY

Based on the classic 1982 arcade game, Moon Patrol, Moon Buggy appeared on the home computers of 1985 amid much praise. It's a cracking Atari game, and it's available in the Linux Terminal by entering:

```
```bash
sudo apt-get install moon-buggy
```
```

Then:

```
```bash
moon-buggy
```
```

Enjoy.

![](bbox=[0.07, 0.88, 0.48, 0.95])

# ### LET IT SNOW

Snowing in the Terminal console isn't something you come across every day. If you're interested, however, enter:

```
```bash
wget https://gist.githubusercontent.com/sentek/
1505483/raw/7d024716e057e69fb52632fee09f42
753631c4d2/snowjob.sh
chmod +x snowjob.sh
./snowjob.sh
```
```

![](bbox=[0.52, 0.88, 0.93, 0.95])