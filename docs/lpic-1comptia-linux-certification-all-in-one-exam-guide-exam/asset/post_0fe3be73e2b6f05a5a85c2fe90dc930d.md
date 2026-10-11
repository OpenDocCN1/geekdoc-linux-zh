
# Working with Environment Variables

Whenever you start a bash shell, several different variables are used to define critical parameters the shell needs to run properly. Because these variables define the shell environment, they are called environment variables. In this part of this chapter, we're going to spend some time learning about environment variables. Specifically, we're going to cover the following topics:

- What environment variables are
- Managing environment variables
- Creating user-defined variables

Let's begin by reviewing what environment variables are.

## What Are Environment Variables?

Before you can understand what an environment variable is, you must first understand what a variable itself is. The best way to describe variables is to envision a bucket in which a variety of substances can be stored. This bucket has a name, such as "MyStuff," and you can fill it with sand, rocks, water, soil, and so on. If the bucket is already full of a particular substance, such as sand, you must empty it before you can fill it with another substance, such as rocks.

You're essentially how a variable in a Linux system works. It's an area in your system's RAM that's reserved to store whatever values you want to put into it. Essentially, it's like a "bucket" in memory. Just as you must empty out a real bucket before you can pour a new substance in, you must also empty out a variable before you can assign a new value to it.

On your Linux system, you can define and use two different types of variables:

- User-defined
- Environment

User-defined variables are just that. They are "buckets" in memory that you create yourself. You can assign user-defined variables with a name of your choice. You can also assign whatever contents you want to them. User-defined variables can be very useful when working with shell scripts, discussed later in this book.

Environment variables, on the other hand, are initially created, named, and populated by the operating system itself. As the name implies, environment variables are used to configure the system's computing environment. Environment variables are frequently accessed and used by programs you run from the shell prompt. Using the information stored in these variables makes these programs much more flexible and robust.

For example, suppose you were to enter the `cd ~` command at the shell prompt. This command will switch the current directory in the shell to the user's home directory, no matter what user is currently logged in.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_85_0.png)

> **NOTE** We will discuss file and directory management commands in depth later in this book.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_86_0.png)

For example, suppose I were logged in to my Linux system as the tracy user account. By default, my home directory would be `/home/tracy`. If I were to enter the `cd ~` command while logged in as tracy, the current directory would be changed to `/home/tracy`. Notice that nowhere in the command did I specify the path `/home/tracy`. The `cd` command just "knew" that `~` pointed to `/home/tracy`. If I were logged in as the ksanders user, however, the same `cd ~` command would not take me to `/home/tracy`. Instead, the current directory would be changed to `/home/ksanders`.

The question is, how does the `cd` command know what directory in the file system to switch to? The `cd` command checked the value of an environment variable named `HOME`. As you can see in Figure 2-17, the value of the `HOME` environment variable is set to the home directory path of the current user.

Because tracy is currently logged in, the value of `HOME` is set to `/home/tracy`. If, however, I were to log in as a user named ksanders, the value of the `HOME` environment variable is changed by the system to `/home/ksanders`. This is shown in Figure 2-18.

Your Linux system defines a number of environment variables like the `HOME` variable we just looked at. Some of the more pertinent environment variables commonly used on most Linux distributions are listed in Table 2-5.

Now that you know what environment variables are and the names of variables commonly used on a Linux system, let’s next discuss how you go about managing your environment variables.

# Managing Environment Variables

For the most part, the values assigned to your environment variables by the system are usually sufficient for most tasks. However, there are occasions when you will need to manipulate the values assigned to your environment variables. To do this, you need to know how to manage them. In this section, we’ll discuss how to do just that. The following topics will be addressed:

- Viewing variables and their values
- Setting the value of a variable
- Making variables persistent

Let’s begin by discussing how to view the value of a variable.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_86_1.png)

| Environment Variable | Stores | Default Value |
| :--- | :--- | :--- |
| BASH and SHELL | The full path to the shell executable | /bin/bash |
| CPU | The type of CPU installed in the system | Depends on your system. An Intel Pentium IV computer would have a value of i686 |
| DISPLAY | The location where your X Window display should be sent | 0.0 (the local video card and monitor) |
| ENV | The name of the file bash read to configure its environment | /etc/bash.bashrc |
| EUID | The user ID (UID) of the current user | The UID number of the current user |
| HISTFILE | The path to the bash command history file | ~/bash_history |
| HISTSIZE | The number of commands saved in the command history file | 1000 |
| HOME | The path to the current user's home directory. | The current user's home directory |
| HOST and HOSTNAME | The hostname of the system | The hostname you assigned when you installed the system |
| LOGNAME | The username of the current user | The username of the current user |
| MAIL | The path to the current user's mailbox file | /var/spool/mail/username or /var/mail/username |
| MANPATH | The path to your system's man program | Depends on the distribution |
| OLDPWD | The path to the prior current directory | Depends on what your prior current directory was |
| OSTYPE | The type of operating system currently being run | Linux |
| PATH | A list of directories to be searched when running a command from the shell prompt | Depends on your distribution |
| PS1 | The characters used to create the shell prompt | Depends on your distribution |
| PWD | The path to the current working directory | Depends on what your current directory is |

Table 2-5 Commonly Used Environment Variables

## Viewing Variables and Their Values

If you need to see the value assigned to a variable on your system, you can use a variety of different commands from the shell prompt. If you need to see the value of a single variable, you can use the `echo` command. The syntax is `echo variable`. For example, if I wanted to view the value of the `PATH` variable, I would enter `echo $PATH` at the shell prompt. This is shown in Figure 2-19.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_88_0.png)

As you can see in Figure 2-19, the contents of the `PATH` variable are displayed on the screen. Notice that when you use the `echo` command you must place a `$` before the name of the variable. This is very important. The `$` character tells the `echo` command that the text that follows is not a literal string but is instead the name of a variable and that echo should retrieve the value of the variable and display it on the screen. If you omit the `$` character, the `echo` command will display your variable name on the screen. For example, if you were to enter `echo PATH` at the shell prompt, the `echo` command will simply display “PATH” on the screen. That’s because it didn’t know that “PATH” was the name of a variable. The `echo` command thought you wanted the text string “PATH” displayed. Don’t forget the `$` character when using `echo` with variables!

As you just saw, the `echo` command works great for displaying the contents of a variable on the screen. However, you can only display the variables you specify. That means you have to know the name of the variables you want to view. What if you don’t know the exact name of the variable? What if you want to view all of your variables at once? In these situations you can use other shell commands to view your variables and their associated values. One of these is the `set` command. If you enter `set` at the shell prompt, all of your variables, including environment and user-defined variables, are displayed on the screen. Because the output of `set` can be very long, you should redirect more with `set` to pause the output displayed one page at a time. (We’ll discuss redirection later in this chapter.) For example, in Figure 2-20, the `set | more` command has been issued at the shell prompt.

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_88_1.png)
