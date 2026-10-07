# Chapter 9: Using Vim

> It might be worth checking the Vim.org Web site to see whether there are newer versions of the syntax files on the Vim.org Web site, as the existing DocBook syntax file is somewhat outdated. (It is written for DocBook 3.0/LinuxDoc.).

![](bbox=[0.063, 0.093, 0.139, 0.199])

# Installing Syntax Files

If you're lucky, your system administrator has been kind enough to install your syntax files and everything for you. If you are your own system administrator, however, you may need to install the syntax files on your own.

Copy the docbook.vim and sgml.vim files to the default /syntax directory. On your system, the /syntax directory is located in /usr/share/vim/vim56/syntax/—but this might differ depending on your distribution.

After you've copied the syntax files to the syntax directory, you will want to edit the .vimrc file to get Vim to automagically use the docbook.vim.

In your home directory, start Vim with the following command:

```
vim .vimrc
```

You'll want to add the following lines to your .vimrc file:

```
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