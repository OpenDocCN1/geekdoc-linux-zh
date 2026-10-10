
![](img/4dec9c51e73c9027d3d8a4fab4408fe6_8_0.png)

*Figure 3: A Linux virtual machine running inside a host OS.*

The result will be a Linux desktop environment (including a command-line terminal program) pre-configured for this tutorial (Figure 3). In the longer run, I recommend switching to a Mac as soon as possible. You might have to save up a bit, as Macs are generally more expensive than Windows machines, but in most cases the increased productivity will quickly pay for the difference. (If you find yourself liking Linux, feel free to stick with it, but Macs are generally easier to use with a better user interface. Plus, you can always run Linux inside a VM, even on a Mac.)

## 1.1 Running a terminal

To run a command-line command, we first need to start a *terminal*, which is the program that gives us a command line. On Macintosh OS X, you can open a terminal window with Spotlight by typing ⌘_ (Command-space) or by clicking on the magnifying glass in the upper right and typing “terminal”; on Linux, you can click the terminal icon as shown in Figure 3. The result should be something like Figure 4, although the exact details on your system will likely differ.

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_9_0.png)

*Figure 4: A terminal window.*

The example we saw in Figure 2 includes all of the typical elements of a command: the prompt followed by a command, an option, and an argument (Figure 5). It’s essential to understand that the prompt is supplied automatically by the terminal, and you do not need to type it. (Indeed, if you do type it, it will likely result in an error.) Moreover, the exact details of the prompt will differ, and are not important for the purposes of this tutorial (Box 3).

If you use OS X and are interested in using a more advanced and customizable terminal program, I recommend installing iTerm, but this step is optional.

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_10_0.png)

*Figure 5: Anatomy of a command line. (Your prompt may differ.)*

### Box 3. What is the prompt?

Every command line starts with some symbol or symbols designed to “prompt” you to action. The prompt usually ends with a dollar sign $, and is preceded by information that depends on the details of your system. For example, on some systems the prompt might look like this:

```
Michael's MacBook Air:~ mhartl$
```

In Figure 4, the prompt looks like this instead:

```
[~]$
```

and in Figure 5 it looks like this:

```
[projects]$
```

Finally, the prompt I’m looking at right now looks like this:

```
[learn_enough_command_line (master)]$
```

For the purposes of this tutorial, the details of the prompt are not important, but we will discuss useful ways to customize the prompt starting in the next tutorial after this one (*Learn Enough*™ *Text Editor to Be Dangerous*).

## Exercises

Learn Enough™ Command Line to Be Dangerous includes a large number of exercises. I strongly recommend getting in the habit of completing them before moving on to the next section, as they reinforce the material we’ve just covered and will give you essential practice in using the many commands discussed.

- 1. By referring to Figure 5, identify the prompt, command, options, arguments, and cursor in each line of Figure 6.
- 2. Most modern terminal programs have the ability to create multiple *tabs*, which are useful for organizing a set of related terminal windows. (For example, when developing web applications, in addition to my main command-line tab I often have separate tabs for running a local web server and an automated test suite.) By examining the menu items for your terminal program, figure out how to create a new tab. *Extra credit:* Learn the keyboard shortcut for creating a new tab. (Learning keyboard shortcuts for your system is an excellent habit to cultivate.)

## 1.2 Our first command

We are now prepared to run our first command, which prints the word “hello” to the screen. (The place where characters get printed is known as “standard out”, which is usually just the screen, and rarely refers to a physical printer.) The command is **echo**, and the argument is the string of characters that we want to print. To run the **echo** command, type “echo hello” at the prompt, and then press the Return key (also called Enter):

```
$ echo hello
hello
$
```

(I recommend always typing the commands out yourself, which will let you learn more than if you rely on copying and pasting.) Here we see that **echo** **hello** prints “hello” and then returns another prompt. Note that, for brevity, I’ve omitted all characters in the prompt except the trailing dollar sign $.

```
[~]$ cd ruby
[ruby]$ ls -a
.           .DS_Store rails
..          projects
[ruby]$ rm -f .DS_Store
[ruby]$ ls -a
.           projects
..          rails
[ruby]$ cd projects/
[projects]$ pwd
/Users/mhartl/ruby/projects
[projects]$ 
```

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_12_0.png)

Just to make the pattern clear, let’s try a second **echo** command:

```
$ echo "goodbye"
goodbye
$ echo 'goodbye'
goodbye
$
```

Note here that we’ve wrapped “goodbye” in quotation marks—and we also see that we can use either double quotes, as in `"goodbye"`, or single quotes, as in `'goodbye'`. Such quotes can be used to group strings visually, though in many contexts they are not required by **echo** (Listing 1).

### Listing 1: Printing “hello, goodbye” two different ways.

```
$ echo hello, goodbye
hello, goodbye
$ echo "hello, goodbye"
hello, goodbye
$
```

One thing that can happen when using quotes is accidentally not matching them, as follows:

```
$ echo "hello, goodbye
>
```

At this point, it seems we’re stuck. There are specific ways out of this quandary (in fact, in this case you can just add a closing quote and hit return), but it’s good to have a general strategy for getting out of trouble (Figure 7). This strategy is called “Ctrl-C” (Box 4).

![](img/4dec9c51e73c9027d3d8a4fab4408fe6_14_0.png)

> *Figure 7: This cat appears to be stuck and should probably hit `Ctrl-C`.*

### Box 4. Getting out of trouble

When using the command line, there are lots of things that can get you in trouble, by which I mean the terminal will just hang or otherwise end up in a state that makes entering further commands difficult or impossible. Here are some examples of such commands:

```
$ echo "hello
$ grep foobar
$ yes
$ tail
$ cat
```

In every case, the solution is the same: hit `Ctrl-C` (pronounced “control-see”). Here `Ctrl` refers to the “control” key on your keyboard, and `C` refers to the key labeled “C”. `Ctrl-C` thus means “While holding down the control key, press C.” In particular, `C` does *not* refer to the capital letter `C`, so you should not press Shift in addition to Ctrl. (`Ctrl-C` sends a *control code* to the terminal and has nothing to do with producing a capital `C` when typing normal text.) The result of typing `Ctrl-C` is sometimes written as `^C`, like this:

```
$ tail
^C
```

The **origins of Ctrl-C** are somewhat obscure, but as a mnemonic I like to think of it as meaning “cancel”. However you remember it, *do* remember it: when you get into trouble at the command line, your best bet is usually to hit `Ctrl-C`.

*Note:* When `Ctrl-C` fails, 90% of the time hitting `ESC` (escape) will do the trick.

## Exercises

- 1. Write a command that prints out the string “hello, world”. *Extra credit:* As in Listing 1, do it two different ways, both with and without using quotation marks.
- 2. Type the command `echo ‘hello` (with a mismatched single quote), and then get out of trouble using the technique from Box 4.

## 1.3 Man pages

The program we’re using to run a command line, which is technically known as a *shell*, includes a powerful (though often cryptic) tool to learn more about
