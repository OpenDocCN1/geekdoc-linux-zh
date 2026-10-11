Notice in Figure 3-5 that there is also a file named `vim` in `/usr/bin` that is also only a symbolic link that points to the `/bin/vim` executable file.

**NOTE** A symbolic link is a shortcut file that points to another file elsewhere in the file system. We’ll discuss symbolic links in depth later in this book.

![](bbox=[0.03, 0.15, 0.15, 0.21])

The result is that no matter what command you type at the shell prompt (`vi` or `vim`), the vim editor is loaded. For example, in Figure 3-6, the `vi` command has been entered at a shell prompt of a Fedora system. Notice, however, that the vim editor has been loaded, as shown in the welcome screen.

With this in mind, let’s discuss how to edit text files in vi.

# ## Editing Text Files in vi

The first time you run vi, you’ll notice right away that its user interface is very different than what you may be used to with other text editors. To familiarize you with vi, we’ll discuss the following topics here:

+   - Opening files in vi
+   - vi modes

![](bbox=[0.1, 0.55, 0.75, 0.85])

**Figure 3-6** Using vim