# Chapter 14 The TC Shell

the original C Shell are now shared by bash, zsh, and tsh. The tsh home page is www.tcsh.org/Home.

Although some of the functionality of tsh is present in bash and zsh, there are differences in the syntax of some commands. For example, the tsh assignment statement has the following syntax:

```
set variable = value
```

Having SPACES on either side of the equal sign, though illegal in bash, is optional in tsh. By convention, shell variables in tsh are generally named with lowercase letters, not uppercase (you can use uppercase). If you reference an undeclared variable (one that has no value assigned to it), tsh will give you an error message whereas bash and zsh will not. The default prompt is a greater sign (>), but Red Hat sets it to a $ character followed by a SPACE. The examples in this chapter use a prompt of tsh $ to avoid confusion with the bash prompt.

# Do Not Use tsh as a Programming Language

If you have used UNIX and are comfortable with the C or TC Shell, you may want to use tsh as your login shell. However, you may find that the TC Shell is not a good programming language as bash or zsh. If you are going to learn only one shell programming language, learn bash. The Bourne Again Shell is used throughout GNU/Linux to program many system administration scripts, including all the scripts in /etc/rc.*

![](bbox=[0.048, 0.595, 0.195, 0.603])

# Shell Scripts

With tsh you can execute files containing TC Shell commands, just as bash and zsh can execute files containing Bourne Again and Z Shell commands. The concepts of writing and executing scripts in the two shells are similar. However, the methods of declaring and assigning values to variables and the syntax of control structures are different.

You can run bash, tsh, and zsh scripts while using any one of the shells as a command interpreter. Various methods exist for selecting the shell that runs a script. Refer to “#! Specifies a Shell” on page 564 for more information.

If the first character of a shell script is a pound sign (#) and the following character is not an exclamation point (!), the TC Shell executes the script under tsh. If the first character is anything other than #, tsh calls bash to execute the script.