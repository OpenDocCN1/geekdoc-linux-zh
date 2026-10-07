
After you have all the necessary files, move them to the /tmp directory (or wherever you like to work with source files), and unzip and untar the files. Follow these steps:

- 1. Execute the following command to become root:

```bash
su -
tar -xvvf vim-x.xx.src.tar.gz
tar -xvvf vim-x.xx.tr.tar.gz
tar -xvvf vim-x.xx.extra.tar.gz
```

- 2. Then unzip and untar the files:

- 3. After you have exploded the packages, you need to change directories to the new directory with the Vim source and other necessary files.

```bash
cd vim-x.xx
```

- 4. After you have entered the new directory, configure and “make” the source files.

```bash
./configure
make
make install
```

> The above instructions should run on any Linux distribution, as well as just about any UNIX variant. However, I do not have access to all the various flavors of Linux, BSD, and UNIX to actually compiling Vim on. If you run into issues, be sure to check the Vim Web site for more information. Also, I'd appreciate an e-mail regarding your experiences on various other flavors of UNIX, to include in future versions of this book.

![](img/81f56bf497dbf7f7582072400d12cb42_214_0.png)

After you've got Vim installed, simply type vim to start Vim.

# Windows and DOS

Vim also comes in Windows and MS-DOS versions. You can find Vim for Windows or MS-DOS on mirror sites in the /packages/vim/pc directory.

To install Vim for Windows, you will need to grab the runtime files, as well as a precompiled binary for the appropriate system.

Unfortunately, Vim versions for Windows tend to lag behind the versions for UNIX and Linux systems. At the time of this writing, Vim 5.7 is available for Linux, and 5.4 is the latest available version for Windows/DOS. Likely, this is because the majority of Vim users are on the Linux- and UNIX- type systems.

# MacOS

Vim users on the MacOS need only to grab the appropriate *.sit file for their Mac. Currently, there are PPC and 68K versions of Vim 5.6 available.

You can find Vim for the MacOS at http://www.symatico.ca/dany.stamant/vim/ (see Figure 9.2).

The Mac version of Vim is pretty much current, and it operates the same way as Vim on other platforms. Figure 9.3 shows Vim running on the MacOS. However, some of the functionality that Vim has on UNIX-type platforms

![](img/81f56bf497dbf7f7582072400d12cb42_215_0.png)

Figure 9.2 The MacVim home page

may be missing because you're not able to call the external UNIX programs from Vim. However, in terms of keybindings and such, MacVim is pretty much the same.

# Using Vim SGML and DocBook Syntax

Now that you have a running version of Vim, it's time to get the syntax files for DocBook.

> If you do a great deal of programming or coding of HTML, you will probably be able to find a Vim syntax file that suits your needs. There are syntax files for HTML, C, Python, Perl, SGML, and many other languages available.

You can find Vim syntax files at http://www.vim.org/lang.html or by simply looking on the CD-ROM included with this book.

# Chapter 9: Using Vim

> It might be worth checking the Vim.org Web site to see whether there are newer versions of the syntax files on the Vim.org Web site, as the existing DocBook syntax file is somewhat outdated. (It is written for DocBook 3.0/LinuxDoc.).

![](img/81f56bf497dbf7f7582072400d12cb42_217_0.png)

# Installing Syntax Files

If you're lucky, your system administrator has been kind enough to install your syntax files and everything for you. If you are your own system administrator, however, you may need to install the syntax files on your own.

Copy the docbook.vim and sgml.vim files to the default /syntax directory. On your system, the /syntax directory is located in /usr/share/vim/vim56/syntax/—but this might differ depending on your distribution.

After you've copied the syntax files to the syntax directory, you will want to edit the .vimrc file to get Vim to automagically use the docbook.vim.

In your home directory, start Vim with the following command:

```bash
vim .vimrc
```

You'll want to add the following lines to your .vimrc file:

```vim
set syntax=on
let color = "true"

if has("syntax")
    if color == "true"
        " This will switch colors ON
        so $($VIMRUNTIME)/syntax/syntax.vim
else
        " this switches colors OFF
        syntax off
        set t_Co=0
endif
```

After you've added these lines to your .vimrc file, you should be able to restart Vim, and whenever you edit DocBook files ending with .sgml or .xml, you'll have color highlighting.

# Using Vim SGML and DocBook Syntax 193

# Basic Vim

Learning Vim will take a bit of practice, but after you've got the hang of it while you will find that you can be quite productive. This section isn't DocBook specific; it's only included only for the convenience of those who haven't gotten the hang of Vim.

![](img/81f56bf497dbf7f7582072400d12cb42_218_0.png)

When you edit text in Vim, whether you're creating a new file or editing an existing one; the text is stored in a buffer—space in memory—you write the changes to a file or discard them. If you start Vim without opening a file to edit, it creates an empty buffer which you begin working. Vim also stores files in a buffer, rather than working directly on them, and changes to the file after a command is written. The practical upset is that you can save it under a different name to avoid changes to the.

# Modal Editors

Vim, like vi, is what known as a modal editor. While using Vim, you are either in the command mode or the insert mode, but unlike most text editors, you can't use both modes at the same time. Vim is designed to enable the user to keep his or her hands on the home keys of the keyboard while using the editor. This design enables users to improve their typing speed greatly because their hands don't have to leave the keys, and thus, a user spends less time trying to use odd keys, such as function keys or mode. Users can delete, cut, paste, search, navigate, and more, by using the standard keys. This requires that the program differentiate when the user is in an insert or append mode and when the user is in a command mode.

Actually, some would say that Vim has three modes: insert mode, command mode, and ex mode—or as the "Getting Started" from the Linux Documentation Project calls it, the last line mode (ex commands from the entered mode combines vi and ex into one handy. However, if ever comes up in a game of Trivial Pursuit, you will be prepared.

# Starting Vim

To begin, put around in Vim a little bit to get the hang of it. Vim (vi should work, too) at the shell prompt, either at the console or in an xterm or its equivalent. Figure 9.4 shows Vim starting up. After you enter an empty buffer, you can type to begin inserting. You are now in insert mode. To leave the insert mode and return to command mode, press the Esc key.

# Chapter 9: Using Vim

![](img/81f56bf497dbf7f7582072400d12cb42_219_0.png)

Figure 9.4 Starting Vim

Now that you're in Vim, try experiment by doing a little editing to get the hang of it.

- 1. If you're not in insert mode already, type i to enter vi's insert mode. There is no visual indication that you have changed modes, unless you set Vim to the No Compatible mode in your vimrc, or by typing inc. The i you've typed doesn't appear unless you type it a second time.

- 2. When in the insert mode, type in a little text so that you have something to experiment with (see Figure 9.5).

- 3. Now that you have some text to play around with, press the Esc key to reenter command mode. Note that it no longer says --INSERT-- at the bottom of the screen (see Figure 9.6). It's not much, but that's how you know that you're in command mode.

- 4. Practice moving around a little bit. You can move around using the arrow keys, but sometimes if you're using Vim on a remote machine, the arrow keys are not recognized properly. Because Vim was
