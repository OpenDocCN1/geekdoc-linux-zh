# **How to prevent the shell from invoking an alias**

*tip* The shell checks only simple, unquoted commands to see if they are aliases. Commands given as relative or absolute pathnames and quoted commands are not checked. When you want to give a command that has an alias but do not want to use the alias, precede the command with a backslash, specify the command's absolute pathname, or give the command as `/.command`.

# **EXAMPLES OF ALIASES**

The following alias allows you to type **r** to repeat the previous command or **r abc** to repeat the last command line that began with **abc**:

```
$ alias r='fc -s'
$ !!
```

If you use the command **ls -ltr** frequently, you can create an alias that substitutes **ls -ltr** when you give the command **l**:

```
$ alias l='ls -ltr'
$ l
total 41
-rw-r--rw- 1 max group 30015 2009-03-01 14:24 flute.ps
-rw-r---rw- 1 max group 3089 2010-02-11 16:24 XTerm.ad
-rw-r---rw- 1 max group 641 2010-04-01 08:12 fixtax.icn
-rw-r---rw- 1 max group 484 2010-04-09 08:14 maptax.icn
drwxrwxr-x 2 max group 1024 2010-08-09 17:41 Tiger
drwxrwxr-x 2 max group 1024 2010-09-10 11:32 testdir/
drwxr-xr-x 1 max group 485 2010-09-21 08:03 floor
drwxrwxr-x 2 max group 1024 2010-09-27 20:19 Test_Emacs
```

Another common use of aliases is to protect yourself from mistakes. The following example substitutes the interactive version of the **rm** utility when you give the command **zap**:

```
$ alias zap='rm -i'
$ zap f*
rm: remove 'fixtax.icn'? n
rm: remove 'flute.ps'? n
rm: remove 'floor'? n
```

The **-i** option causes **rm** to ask you to verify each file that would be deleted, thereby helping you avoid deleting the wrong file. You can also alias **rm** with the **rm -i** command: **alias rm='rm -i'**.

The aliases in the next example cause the shell to substitute **ls -l** each time you give an **ll** command and **ls -F** each time you use **ls**:

```
$ alias ls='ls -F'
$ alias ll='ls -l'
$ ll
total 41
drwxrwxr-x 2 max group 1024 2010-09-27 20:19 Test_Emacs/
drwxrwxr-x 2 max group 1024 2010-08-09 17:41 Tiger/
-rw-r---rw- 1 max group 3089 2010-02-11 16:24 XTerm.ad
-rw-r---rw- 1 max group 641 2010-04-01 08:12 fixtax.icn
-rw-r---rw- 1 max group 30015 2009-03-01 14:24 flute.ps
-rwxr-xr-x 1 max group 485 2010-09-21 08:03 floor*
-rw-r---rw- 1 max group 484 2010-04-09 08:14 maptax.icn
drwxrwxr-x 2 max group 1024 2010-09-10 11:32 testdir/
```