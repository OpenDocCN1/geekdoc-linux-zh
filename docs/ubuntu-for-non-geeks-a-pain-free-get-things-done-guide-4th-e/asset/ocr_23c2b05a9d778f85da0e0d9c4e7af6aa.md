# 9B-9: Adding Emblems to Your LocalApps Folder

Now that pyWings is successfully installed and working, it is probably a good idea to add an emblem to your new LocalApps folder so that you don’t inadvertently dump it in the Trash someday. You already learned how to do this in Chapter 8, so I won’t give you the step-by-step instructions.

# Project 9C: Command Practice Review with Briscola

If you want to reinforce the skills you’ve put to use in the previous project, why not go a bit Continental and try Briscola—a simple, yet very traditional, Italian card game (see Figure 9-15)? Unlike pyWings, which is a Python script, Briscola is a script of a different flavor, written in a scripting language called Tcl, which uses something called Tk to create its graphical interface.

![](bbox=[0.22, 0.4, 0.78, 0.73])

Figure 9-15: Briscola

# 9C-1: Getting Briscola

You are just about ready to begin “installing” Briscola, but before you do, you must get it. You can get Briscola by going to the project’s home page at http://www.rigacci.org/comp/software/ and downloading it in the traditional manner, but since we’re working with commands, let’s instead get Briscola by using a new command: wget.

To do this, just open a Terminal window, type the following command string, and then press ENTER:

```
wget http://www.rigacci.org/comp/software/briscola/briscola-4.1.tar.gz
```