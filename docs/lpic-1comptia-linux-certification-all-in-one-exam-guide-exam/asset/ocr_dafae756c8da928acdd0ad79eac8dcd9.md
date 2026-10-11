+   B. At the shell prompt, enter export PS1.
+   
+   C. At your shell prompt, enter ls \~ -a. Which file would you edit on your particular distribution if you wanted to make the changes to your PS1 environment variable persistent?

With this in mind, let’s now talk about creating user-defined variables.

# Creating a User-Defined Variable

In the preceding topic, we’ve focused on working with environment variables. These variables are automatically defined for you each time the system boots. However, you can actually create your own customized variables as well. This is done in exactly the same way as when managing environment variables. Simply enter variable=value at the shell prompt.

For example, suppose I wanted to create a variable named ME and set it to a value of “Robb Tracy”. I can do this by entering ME="Robb Tracy" at the shell prompt. Once I do this, a variable named ME is added to my system and is set to a value of Robb Tracy. You can use the echo command to view the value of the ME variable, as shown here:

```
rtrace@fs2:~> ME="Robb Tracy"
rtrace@fs2:~> echo $ME
Robb Tracy
rtrace@fs2:~> 
```

As with environment variables, a user-defined variable is available only to the current instance of the shell. To make it available to other shells, including subshells created by the current shell, you need to export it with the export command. In this example, I would enter export ME at the shell prompt to do this. In addition to echo, you can also use set or env to view user-defined variables just as you did with environment variables.

As with environment variables, you can make a user-defined variable persistent by adding the appropriate commands to one of the bash configuration files discussed previously. When creating user-defined variables, keep the following rules in mind:

+   - Variable names can contain letters or numbers, but they may not begin with a number.
+   - Variable names may contain hyphens (-) or underscore characters (\_).
+   - While not required, you should try to use all uppercase characters when naming your variables. Notice when you enter set or env that all of your system’s environment variables use uppercase names. You should do the same.

The next topic we need to address is that of aliases. Let’s discuss how aliases work next.