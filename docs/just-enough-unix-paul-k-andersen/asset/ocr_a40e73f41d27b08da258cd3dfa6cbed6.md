# ## 5.11 Creating a File by Redirection

The second method of creating a new file is to redirect the output of a command. In other words, instead of displaying the results of the command on the screen, UNIX puts the results into a file. As an example, consider what happens if Jill moves to her Marsupials directory and issues the `ls` command:

```
`$ ls (Return)`
```

```
bandicoot  kangaroo  opossum  wombat
```

Suppose now that she wants to redirect this list into a file named `filelist`. She does this using the *output redirection symbol* `>`:

```
`$ ls > filelist (Return)`
`$`
```

This time, nothing appears on the screen because the output was rerouted into the file. In UNIX terminology, the information was redirected from the *standard output* (the terminal screen) to the file. If Jill lists her files now, she will see that there is a new one named `filelist` in the directory:

```
`$ ls (Return)`
`bandicoot  filelist  kangaroo  opossum  wombat`
```

Redirection is powerful and convenient, but it can be dangerous. If you redirect the output into a file that already exists, the original contents of the file will be lost. If you want to add something to the end of an existing file without losing the original contents, you can use the *append* operation, which requires two redirection symbols (`>>`):

```
`$ ls >> filelist (Return)`
`$`
```

# ## 5.12 Access Privileges

The UNIX operating system is designed to make it easy for users to share files. However, there are times when you do not want others to copy, move, or even examine the contents of your files and directories. You can easily control access to the files in your home directory. To see how this is done, refer to Appendix D, “Access Privileges.”