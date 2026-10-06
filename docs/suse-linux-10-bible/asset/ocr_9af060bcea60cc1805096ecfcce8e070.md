# Using the vim Initialization File

If you want to customize how vim works, you can add startup commands to the file .vimrc in your home directory. This file is used to set the profile for how vim works for you and is a very useful.

One popular feature of vim is its syntax highlighting. If you are editing C, or maybe Perl, vim can colorize your text so it is easier to read. Open the .vimrc file (it may not exist, which means you'll have to create it) and add the following to the file:

```
syntax on
```

It is usually nice to be able to use the Backspace key to delete characters for folks who like to be able to edit interactively.

```
set backspace=2
```

This tells vim when it is in insert mode, the Backspace key can be used to delete text as you do in Windows Notepad, for example.

And finally for programmers out there, it is useful to indent your code when typing so that your structure remember the current place you are indented by setting the autoindent parameter in your startup file:

```
set autoindent
```

Now, when you press Enter for a new line, vim returns to the column you are indented (using the Tab key).

You can set many options in your .vimrc file, and it would take a whole book to describe them all. An excellent vim tutorial at http://newbiedoc.sourceforge.net/tutorials/vim/index-vim.html can be of help.

# Exiting vim

To exit vim, you need to use the :q command. This will quit the current session as long as you have saved your work (that is, all text buffers are written to disk).

If you want to quit and save the current file to disk, use :wq. This works only if you have assigned a filename to the file you are working with. If you have not, you will get an error message. To remedy this, you can pass the name of the file you want to save with :wq filename. In the case of the example file we used previously in this section, entering :wq /home/justin/mynfile will successfully save the file and exit vi cleanly.