The following commands show two ways for Max to create the **promo** directory as a child of the newly created **literature** directory. The first way checks that **/home/max** is the working directory and uses a relative pathname:

```
$ pwd
/home/max
$ mkdir literature/promo
```

The second way uses an absolute pathname:

```
$ mkdir /home/max/literature/promo
```

Use the **-p** (parents) option to **mkdir** to create both the **literature** and **promo** directories with one command:

```
$ pwd
/home/max
$ ls
demo   names   temp
$ mkdir -p literature/promo
```

or

```
$ mkdir -p /home/max/literature/promo
```

# cd: CHANGES TO ANOTHER WORKING DIRECTORY

The **cd** (change directory) utility makes another directory the working directory; it does not *change* the contents of the working directory. The following examples show two ways to make the **/home/max/literature** directory the working directory, as verified by **pwd**. First Max uses **cd** with an absolute pathname to make **literature** his working directory—it does not matter which is the working directory when you give a command with an absolute pathname. A **pwd** command confirms the change Max made.

```
$ cd /home/max/literature
$ pwd
/home/max/literature
```

When used without an argument, **cd** makes your home directory the working directory, as it was when you logged in. The following **cd** command does not have an argument, so it makes Max’s home directory the working directory. Finally, knowing that he is working in his home directory, Max uses a simple filename to make the **literature** directory his working directory (**cd literature**) and confirms the change using **pwd**.

```
$ cd
$ pwd
/home/max
$ cd literature
$ pwd
/home/max/literature
```