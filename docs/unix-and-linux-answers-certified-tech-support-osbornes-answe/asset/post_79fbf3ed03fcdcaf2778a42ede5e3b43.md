
Or it can be the result of running a program or even a series of programs. In this case the result or return code of the final program will be evaluated for the condition. An example might be something like

```
if echo $PATH | grep X11
```

which will test true if the path includes "X11" anywhere in it. This could also be a "multiple choice test":

```
if ( echo $PATH | grep interbase ) || whence gdml
```

This will test to see if the path contains "interbase" or if one of its programs, gdml, can be found. If either is true, then the condition will be true.

## Can you show me how to use for loops in the Korn shell?

The for construct lets you perform an operation a fixed number of times. This is useful when you need to perform an operation on a group of items, such as a list of filenames. This is a bit different from how a C or Pascal programmer might expect a for loop to behave. In that case, the syntax might be something like: for i=1 to 10 do. Here we're passing a list of items to a variable, changing the value of the variable each time the loop is run. The syntax for this construct is

```
for name in [list]
do
statements that act on or use $name
done
```

Each time through the loop, the value of $name has a different value, as it goes through the items in list one at a time.

## What do I need to know about using while and until loops in the Korn shell?

The while loop combines a conditional test with a looping construct, and as long as the condition tests true, the loop will continue to run. Think about that for a moment. If you
depending on what kind of file it is, do something different with the file. So you could take output from a find command, for example, that found every file that you hadn’t changed in the last month to create a filelist, and then do something with those files, depending on what sorts of files they were. You could remove all of them with "tmp" in the name, move any with "sav" in the name to an archive directory, and so forth. Figure 13-2 shows a script to do just that.

## How should I use the select statement?

The Korn shell’s select construct is a unique way to build a simple menu and branch based on the response to that menu. The select statement doesn’t really line up with any corresponding statement in C or Pascal or any other language we know about. But it certainly makes it easy for you to do things that might otherwise be a nuisance. The basic syntax of select is

```
select var [in list]
do
    statements that act on or use $var
 done
```

![](img/0c1fc10350aa06ca92e7921c96c628ec_240_0.png)

Figure 13-2 Case lets you do different things with different files, all in one easy to understand statement

## Chapter 13  The Korn Shell

This looks a lot like the syntax of a **for** loop, and it should because they are, in fact, the same. The difference is that with the **select** construct we don’t pass everything in the list to the do...done part, only what the user selects from the menu that’s displayed. Figure 13-3 shows an example of how this works.

```
cat pets
PS3='favorite pet? '
select var in Cats Dogs Birds Fish
do
        case $var in
                Cats)   print "Cats are my favorite pet";;
                Dogs)   print "Dogs make friendly pets";;
                Birds)  print "Birds are a cheerful addition to the house";;
                Fish)   print "Fish make for a quiet pet";;
        esac
        break
done
$ pets
1) Cats
2) Dogs
3) Birds
4) Fish
favorite pet? 1
Cats are my favorite pet
```

![](img/0c1fc10350aa06ca92e7921c96c628ec_241_0.png)

**Figure 13-3**  The Korn shell’s select builds simple menus automatically

## Chapter 14

## Linux

## Answer Topics!

- **LINUX BASICS** 214
  - ? Where to get Linux
  - ? Is Linux a real UNIX
  - ? Favorite Linux distribution
  - ? Other Linux distributions
  - ? Why Linux is free

- **KEYBOARD ISSUES** 217
  - ? Modifying the keyboard
  - ? Editing keytables
  - ? Editing the default keytables for power users
  - ? How keytables work
  - ? Meta keys

- **PASSWORD SECURITY** 220
  - ? Linux and password security

- **SHELLS** 221
  - ? Shells offered in Linux
  - ? The bash startup files
  - ? Displaying the current directory in the shell prompt

- **TEXT EDITORS** 224
  - ? Standard Linux text editors

- **LINUX AND X WINDOWS** 224
  - ? Using a graphical interface in Linux
  - ? Accessing the graphical login screen
  - ? Configuring XDM
  - ? Starting up permanently in X Windows
  - ? Understanding widgets
  - ? Why widgets are important
  - ? Customizing FVWM
  - ? Understanding focus policy
  - ? Making FVWM look like the motif window manager (mwm)
  - ? Changing colors in FVWM
  - ? Useful settings for FVWM
  - ? Other window managers for Linux
  - ? Customizing your keyboard under X Windows
  - ? Changing the title bar of xterms

- **OTHER TOOLS THAT ARE DIFFERENT UNDER LINUX** 235
  - ? Some tools that are different under Linux
