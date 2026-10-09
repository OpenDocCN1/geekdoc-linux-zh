If you are not working in /usr/src, you must copy the linux-source* file to the directory you are working in; otherwise, cd to /usr/src. Use tar to unpack the Linux source file:

```
$ tar -xjf linux-source-2.6.32.tar.bz2
```

# git: Obtaining the latest kernel source code

The git utility (GNU interactive tools, git-scm.com) can download the latest versions of the source code for several different kernels and can keep that source code up-to-date. If it is not already installed, give the following command to install git:

```
$ sudo aptitude install git-core
```

# Install the git-core package, not the git package

> Make sure to install the **git-core** package and not the **git** package. The **git** package is not useful for downloading kernel source code.

The following command uses git to download a copy of the development (not the released) kernel into the **ubuntu-2.6** subdirectory of the working directory. As a member of the src group, you can work in the /usr/src directory. Otherwise, you can work in any directory you have write access to. You can and should work as a nonprivileged user.

```
$ git clone git://kernel.ubuntu.com/ubuntu/Ubuntu-lucid.git ubuntu-2.6
Initialized empty Git repository in /home/sam/ubuntu-2.6/.git/
remote: Counting objects: 1624172, done.
remote: Compressing objects: 100% (292458/292458), done.
remote: Total 1624172 (delta 1346815), reused 1590040 (delta 1315854)
Receiving objects: 100% (1624172/1624172), 468.69 MiB | 392 KiB/s, done.
Resolving deltas: 100% (1346015/1346015), done.
Checking out files: 100% (31201/31201), done.
```

See kernel.ubuntu.com/git and git.kernel.org for a list of Ubuntu kernels you can download. Substitute the URL of the kernel you want to download for the URL in the preceding command and specify the name of an appropriate directory to hold the files you download. For example, the following command downloads the latest Jaunty kernel into the jaunty directory in the working directory:

```
$ git clone git://kernel.ubuntu.com/ubuntu/Ubuntu-jaunty.git jaunty
```

Once you have downloaded the kernel, cd to the directory that holds the code and give the following command to update the source code to match that available at the URL you specified in the git-clone command:

```
$ git pull
Already up-to-date.
```

The files you just downloaded should be up-to-date, as shown in the example. Give this command any time you want to synchronize the code in the working directory with the latest source code at the URL.