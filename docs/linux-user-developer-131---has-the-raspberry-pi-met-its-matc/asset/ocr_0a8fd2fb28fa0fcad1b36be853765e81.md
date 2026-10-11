# Questions & answers

**Contact us...**

Web: www.linuxuser.co.uk
Email: linuxuser@imagine-publishing.co.uk

Facebook: Linux User & Developer

Twitter: @linuxusermag

# # Your questions
# answered

**ASK THE EXPERTS**
Send us your questions and we'll do our best to answer them!

This month your questions were answered by...

![](bbox=[0.06, 0.38, 0.13, 0.46])

**Russell Barnes** has been a computer and technology journalist for nearly 15 years

![](bbox=[0.06, 0.5, 0.13, 0.58])

**Rob Zwetsloot** studied aerospace engineering, using Python to model simulations

![](bbox=[0.06, 0.62, 0.13, 0.7])

**Kunal Deo** is a veteran developer of many open source projects

![](bbox=[0.06, 0.75, 0.13, 0.83])

**Richard Smedley** spends 90% of his screen time shelled into servers in the UK and USA

![](bbox=[0.35, 0.35, 0.93, 0.57])

Clonezilla is a powerful disc imaging tool

# ## How do I compile software?

Compiling software from source code isn't that difficult – all it requires are simple build tools available in all repos. To make sure you have the correct build tools installed, do the following on a Debian-based system:

```
$ sudo apt-get install build-essentials
```

Alternatively, for other systems, use:

```
$ sudo yum groupinstall 'Development Tools'
```

Once you have the necessary source code for the software you want to compile, navigate to the folder in the terminal and type:

```
$ . /configure
```

...to build the files, and follow up with:

```
$ make
```

...to compile it.

# ## Ghost editing

Hi there. I've been playing around with my system recently, and decided to do a small overhaul of my disc setup. I created a ghost of my main hard drive, which was not full, and am now attempting to apply it to a smaller space than it was originally on.

I figure because the image wasn't full up anyway (and there was no important data I'll lose if I start messing about with it) that I can make some changes to the file and be able to apply it to the new disc I want it to be on? Hope you have some answers.

Joe O'Reilly

88

www.linuxuser.co.uk