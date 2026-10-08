An example of this functionality:

```
>split -l 3 boot.msg splitfile
```

The boot.msg file from the previous example has been run through split and has been divided into two files of three lines each. The -l option specified the 3 lines each. It's important to know this command if you want to break data down into manageable chunks so that you can either work with them or send them to others.

You may be wondering how you reassemble a file you break and split it up. You can do this with a previously learned command, the cat command.

You need to reassemble your files that you just split. To do this, you need to use the cat command. When you have a series of files named with something as <name> <name=aa, <basename=ab, <basename=ac<basename=zz>, you can reassemble them by issuing the cat command as follows: cat <basename>* > combine_complete.file. This will reassemble your files so that you can work with them.

 Another set of utilities will you come to love is the patch and diff commands. These utilities will also help you with your Unix file management.

# The diff and patch Commands

The diff and patch commands are a pair so we will cover them here together. Because of how they work, we will cover diff first.

When using diff, you will take two files, the original template and an updated file that produces an output file. This file will contain enough information within it to be able to reconstruct the updated file when only given the patch file and template file. This can be handy if you want to only send out updates to, for example, a book, as you could send the edits of sending the entire file and replacing it. For smaller files this may not be a big deal, but for larger files that are of substantial size and may have multiple people working on them, using diff may be very helpful to you.