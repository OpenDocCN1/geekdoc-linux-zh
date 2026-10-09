# **Page breaks for the printer**

CONTROL-L tells the printer to skip to the top of the next page. You can enter this character anywhere in a document by pressing CONTROL-L while you are in Input mode. If `^L` does not appear, press CONTROL-V before CONTROL-L.

# ## ENDING THE EDITING SESSION

While you are editing, vim keeps the edited text in an area named the *Work buffer*. When you finish editing, you must write out the contents of the Work buffer to a disk file so that the edited text is saved and available when you next want it.

Make sure vim is in Command mode, and use the `ZZ` command (you must use uppercase *Zs*) to write your newly entered text to the disk and end the editing session. After you give the `ZZ` command, vim returns control to the shell. You can exit with `:q!` if you do not want to save your work.

# **Do not confuse `ZZ` with `CONTROL-Z`**

When you exit from vim with `ZZ`, make sure that you type `ZZ` and not `CONTROL-Z` (typically the suspend key). When you press `CONTROL-Z`, vim disappears from your screen, almost as though you had exited from it. In fact, vim will continue running in the background with your work unsaved. Refer to “Job Control” on page 307. If you try to start editing the same file with a new vim command, vim displays a message about a swap file.

# ## THE COMPATIBLE PARAMETER

The **compatible** parameter makes vim more compatible with vi. By default this parameter is not set. From the command line use the `-C` option to set the **compatible** parameter and use the `:-N` option to unset it. To get started with vim you can ignore this parameter.

Setting the **compatible** parameter changes many aspects of how vim works. For example, when the **compatible** parameter is set, the Undo command (page 192) can undo only your most recent change; in contrast, with the **compatible** parameter unset, you can call Undo repeatedly to undo many changes. To obtain more details on the **compatible** parameter, give the command `:help compatible` RETURN. To display a complete list of vim’s differences from the original vi, use `:help vi-diff` RETURN. See page 190 for a discussion of the `help` command.

# ## CHAPTER SUMMARY

The utilities introduced in this chapter are a small but powerful subset of the many utilities available on an Ubuntu Linux system. Because you will use them frequently and because they are integral to the following chapters, it is important that you become comfortable using them.