![](bbox=[0.46, 0.07, 0.75, 0.31])

Figure 7-6 Redirecting standard output

where command is any executable program (such as an application program or a utility), arguments are optional arguments, and filename is the name of the ordinary file the shell redirects the output to.

Figure 7-7 uses cat to demonstrate output redirection. This figure contrasts with Figure 7-5, where both standard input and standard output are associated with the keyboard and the screen. The input in Figure 7-7 comes from the keyboard. The redirect output symbol on the command line causes the shell to associate cat's standard output with the sample.txt file specified on the command line.

After giving the command and typing the text shown in Figure 7-7, the sample.txt file contains the text you entered. You can use cat with an argument of sample.txt to display this file. The next section shows another way to use cat to display the file.

# Redirecting output can destroy a file!

> caution Use caution when you redirect output to a file. If the file exists, the shell will overwrite it and destroy its contents. For more information see the tip "Redirecting output can destroy a file !" on page 236.

Figure 7-7 shows that redirecting the output from cat is a handy way to create a file without using an editor. The drawback is that once you enter a line and press RETURN, you cannot edit the text. While you are entering a line, the erase and kill keys work to delete text. This procedure is useful for making short, simple files.

```
```
$ cat > sample.txt
This text is being entered at the keyboard and
cat is copying it to a file.
Press CONTROL-D to indicate the
end of file.
CONTROL-D
$
```
```

Figure 7-7 cat with its output redirected