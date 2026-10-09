
Now, enjoy the show!

It goes without saying that this particular Linux server is atypical—however, you will use a very similar process, either in `PuTTY` or on the command line, to connect to any remote Linux server.

## Task 4:

Finally, locate the Terminal application. When you launch Terminal, it runs a special application called a shell. The default and most common shell is called `Bash`, but there are other options.

In practice, you will most often use the Terminal directly rather than a GUI application like `PuTTY`.

## Notes:

Though less important on a modern desktop machine, the shell is a critical feature for managing Linux servers. In future labs, we will dive into the shell.

# LAB 4

## Open Source Software and Licensing

**Lab Objective:**

Learn about open source philosophy and different forms of open source software licensing.

**Lab Purpose:**

When working with open source software, particularly in business, it is important to recognize the implications of various licenses and business models.

**Lab Tool:**

A device with a web browser

**Lab Topology:**

N/A

**Lab Walkthrough:**

### Task 1:

Explore `chooselicense.com` and try to answer the following questions:

- What is the difference between a copyleft license and a permissive license?

- What are the differences between `GPL`, `BSD`, and Creative Commons?

- Which licenses are compatible with each other when packaging software (and which ones aren't)?

### Task 2:

Next, consider or read about some potential open-source business models. Can you identify how each business/service below monetizes open source software?

- `Apple`

- `Canonical`

- `Mozilla`

- `MySQL` (`Oracle`)

- `RedHat`

- `Wikipedia`

- `WordPress`

**Notes:**

Keep in mind that some potential business models are considered unethical by many members of the open-source community.

# LAB 5

## ICT Skills and Working in Linux

**Lab Objective:**

Make your Linux VM “your own” by doing some basic configuration and learning how to use common tools.

**Lab Purpose:**

The goal of this lab is to learn how to do some simple customizations of common Linux tools.

**Lab Tool:**

`Ubuntu` 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Open the `Firefox` web browser and explore its configuration. Click the menu in the upper-righthand corner, then click `Preferences`.

Consider tweaking some of `Firefox`’s privacy and security settings. For example:

- Are all trackers and third-party cookies blocked by default?

- What is the default search engine? Is that acceptable to you?

- What kind of data does `Firefox` collect on you? Would you like to change that?

- What are the history and password-saving settings?

### Task 2:

Now, you might like to install an add-on to `Firefox`. Use the search engine you chose to look for an add-on that might enhance `Firefox` in some way. Ad blocking, tab management, development tools, there are plenty of options!

### Task 3:

If you haven't already, add the Terminal application in `Ubuntu` to your Favorites. You'll be using it a lot!

1. Click “Show Applications” in the bottom left corner, and search for `Terminal`.

2. Right-click the `Terminal` application and click “Add to Favorites”.

### Task 4:

Now we're going to change your `Ubuntu` password, via the command line. Open the Terminal application, then enter: `passwd`

You will first need to type your current password, then type your new password twice. None of these passwords will show anything being typed at all, which can be a bit jarring at first! However, in the end, you should see the message: `passwd: password updated successfully`

**Notes:**

So far in these labs, you have primarily used the desktop form of Linux. However, in industry, Linux has a far larger share on servers. How do large tech companies and industry professionals typically use Linux, and virtualization, on a daily basis?

# LAB 6

## Command Line Basics: Syntax and Quoting

**Lab Objective:**

Learn basic Linux commands and shell syntax.

**Lab Purpose:**

The `Bash` command shell is pre-installed on millions of Linux computers around the world. Understanding how this shell works is a critical skill for working with Linux.

**Lab Tool:**

`Ubuntu` 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Open the Terminal application, then enter: `echo Hello World`

The `echo` command simply prints out all of the "words," or arguments, that you give to it. This might not seem very useful, until...

### Task 2:

Now enter the following four commands, in order:

```bash
quote='cat /etc/issue'
backquote=`cat /etc/issue`
echo $quote
echo $backquote
```

Here, `quote` and `backquote` are called variables. In the first two lines, we set them to the values `'cat /etc/issue'` and `` `cat /etc/issue` ``, respectively. (We'll get to the difference between quotes and backquotes in a minute.) In the last two lines, we reference the variables by putting `$` before them, and print out their contents.

### Task 3:

To understand single quotes, double quotes, and backquotes, enter the following:

```bash
hello="echo hello"

echo "$hello"

echo '$hello'

echo `$hello`
```

The output should be as follows:

```
echo hello
$hello
hello
```

Double quotes allow for variables to have their values referenced. Single quotes are always literal, while backquotes execute the command (including variable references) within those quotes.

## Notes:

In some cases, you will want to reference variables with the `${variable}` syntax. This is equivalent to `$variable`, but the reasons for choosing one over the other are beyond the scope of this lab.

Backquotes also have an alternative syntax:

```bash
$(echo hello)
```

This syntax is generally preferred over backquotes. We only mention backquotes to distinguish them from single quotes and ensure the differences are clear.

# LAB 7

## Command Line Basics: Environment Variables, Types, and History

**Lab Objective:**

Learn about `Bash` environment variables, types, and how to use the shell history.

**Lab Purpose:**

The `Bash` command shell is pre-installed on millions of Linux computers around the world. Understanding how this shell works is a critical skill for working with Linux.

**Lab Tool:**

`Ubuntu` 18.04 (or another distro of your choice)

**Lab Topology:**

A single Linux machine, or virtual machine

**Lab Walkthrough:**

### Task 1:

Open the Terminal application, then enter: `echo $PATH`

The `PATH` environment variable lists all locations that `Bash` will search when you enter a command with a relative path. A relative path example is `bash`, compared to `/bin/bash`, which is an absolute path.

There are other environment variables as well. You can view all of them, and their values, using the `env` command.

### Task 2:

You can add or modify an environment variable with `export`. For example:

```bash
export PATH=$PATH:./
```

In most cases, this change will disappear when you exit `Bash`, but the advantage of `export` is that child processes will now be able to see the new/modified variable.

### Task 3:

Another useful `Bash` command is called `type`. Use `type` to figure out information on other commands or functions:

```bash
type -a date
type -a if
type -a echo
type -a ls
```

### Task 4:

Enter `history` to see a history of commands you have typed into `Bash`.

To repeat a command, simply enter `!` and then the appropriate number. For example, `!12` will execute command `#12` in the history list.

If you accidentally saved a password or other sensitive information to the history, you may use, for example, `history -d 47` to delete command #47 from the list, or even `history -c` to clear the history altogether.

If you want to save your current shell's history to another file, use `history -w filename`

## Notes:



If you wish to permanently modify an environment variable or other shell settings, look into the `.bashrc` and `.bash_profile` files.
