Let’s suppose you want to go into a subdirectory of your home directory. We can **cd** back to your home directory and then **cd** into a subdirectory called **book**:

```
```
darkstar:/$ cd /home/fido
darkstar:/home$ /home/fido
darkstar:~$ cd book
darkstar:/book$ pwd
/home/fido/book
```
```

In this case, we used **cd** to get back **home** (verified with the **pwd** command), then told Linux to make the subdirectory **book** our current directory. We know the directory **book** is below our home directory, so we used relative filenames to move into it. We could have specified the absolute pathname, too, but this was much easier. To avoid any confusion or mistakes, use the absolute directory names when using the **cd** command:

```
```
darkstar:/$ cd /usr/bin
darkstar:/usr/bin$ pwd
/usr/bin
```
```

When you type an absolute directory name, you go to that directory, no matter where you started from. When you type **cd ..**, where you end up depends on where you started.

To see the effect of changing your working directory, type **ls**. The list of files is so long that the first part scrolls off your screen. The **ls** command shows you the contents of your current directory (as always), but now your current directory is /usr/bin, which contains many more files than your home directory.

# ## There’s No Place Like Home

Here’s a handy trick that many UNIX and Linux users don’t use. Type **cd** without any directory specification:

```
```
darkstar:/usr/bin$ cd
darkstar:~$ pwd
/home/fido
```
```

Typing **cd** by itself always returns you to your home directory, no matter where you are when you type **cd**. When exploring the file system, you sometimes wind up deep in a blind alley of subdirectories. Type **cd** to quickly return home or type **cd /** to return to the root directory.

The “-” in your prompt is another special character. It stands for your home directory. There’s no reason to type **cd -** when **cd** works just as well, and is much easier to type! A tilde (“~”) by itself indicates your own home directory.