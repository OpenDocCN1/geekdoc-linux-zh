![](bbox=[0.1, 0.1, 0.9, 0.47])

**Fig. 13.1** The *tiger* Directory Tree

*tiger* to *Run through cron* on page 368). The *tigexp* script provides verbose explanations for *tiger* message IDs and is described in *Deciphering tiger Output* on page 373.

Moving on to the directories used by *tiger*, the *bin* directory will hold binaries that *tiger* may use during execution. These are described in Table 13.2 on page 347. The *c* directory holds the source code for these binaries. Explanatory messages used by *tiger* security reports are stored in files under the *doc* directory. These are used by scripts discussed in *Deciphering tiger Output* on page 373 and are covered in more detail in *Modifying tiger* on page 375. The *man* directory contains man pages for the *tiger* and *tigexp* scripts. You may view these by installing them in your system man directory or by executing the command

```
nroff -man *filename* | more
```

or

```
man *filename*
```

where you would replace *filename* with /usr/src/tiger/man/tiger.8 or /usr/src/tiger/man/tigexp.8.

The *scripts* directory contains the meat of the code used by *tiger*. Here you will find Bourne-shell code used to generate the security report. Helper scripts, which are not callable directly, reside in the *sub* and *misc* subdirectories.