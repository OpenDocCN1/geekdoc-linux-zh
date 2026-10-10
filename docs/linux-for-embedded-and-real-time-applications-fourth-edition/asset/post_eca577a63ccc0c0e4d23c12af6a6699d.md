
## Listing 3.1
# Trivial example of fork.

```c
#include <unistd.h>
#include <stdio.h>

pid_t pid;

void do_child_thing(void)
{
    printf("I am the child. My PID is %d\n", pid);
}

void do_parent_thing(void)
{
    printf("I am the parent. My child's PID is %d\n", pid);
}

void main(void)
{
    switch (pid = fork())
    {
        case -1:
            printf("fork failed\n");
            break;
        case 0:
            do_child_thing();
            break;
        default:
            do_parent_thing();
    }
    
    exit(0);
}
```

If `execve()` succeeds, it does not return. Instead, control is transferred to the newly-loaded program.

# The Linux File System

The Linux file system is in many ways similar to the file system you might find on a Windows PC or a Macintosh. It is a hierarchical system that lets you create any number of subdirectories under a *root directory* identified by “/.” Like Windows, file names can be very long. However, in Linux, as in most Unix-like systems, filename “extensions,” the part of the filename following “...”, have much less meaning than they do in Windows. For example, while Windows executables always have the extension “.exe,” Linux executables rarely have an extension at all. By and large, the contents of a file are identified by a file header, rather than a specific extension identifier. Nevertheless, many applications, the C compiler for example, do support default file extensions.

## Listing 3.2
# Command line interpreter.

```c
#include <unistd.h>
#include <stdio.h>

void main (void)
{
    char *argv[10], *filename;
    char text[80];
    char foreground;
    pid_t pid;
    int status;
    while (1)
    {
        gets (text);
        // Parse the command line to derive filename and
        // arguments. Decide if it's a foreground command.
        switch (pid = fork())
        {
            case -1:
                printf ("fork failed \n");
                break;
            case 0: // child process
                if (execve (filename, argv, NULL) < 0)
                    printf("command failed \n");
                break;
            default: // parent process
                if (foreground)
                    waitpid (&status, pid);
        }
    }
}
```

Unlike Windows, file names in Linux are *case-sensitive*. `FooBar` is a different file from `foobar`, is different from `fooBar`. Sorting is also case-sensitive. File names beginning with upper case letters appear before those that begin with lower case letters in directory listings sorted by name. File names that begin with “.” are considered to be “hidden,” and are not displayed in directory listings unless you specifically ask for them.

Additionally, the Linux file system has a number of features that go beyond what you find in a typical Windows system. Let us take a look at some of the features that may be of interest to embedded programmers.

# File Permissions

Because Linux is multiuser, every file has a set of *permissions* associated with it to specify what various classes of users are allowed to do with that file. Get a detailed listing of some Linux directory, either by entering the command `ls -l` in a command shell window, or with the desktop file manager. Part of the entry for each file is a set of 10 flags and a pair of names that look something like this:

```
-rw-r-r-- Andy physics
```

In this example, Andy is the *owner* of the file, and the file belongs to a *group* of users called physics, perhaps the physics department at some university. Generally, but not always, the owner is the person who created the file.

The first of the 10 flags identifies the file type. Ordinary files get a dash here. Directories are identified by “d,” links are “l,” and so on. We will see other entries for this flag when we get to device drivers later. The remaining nine flags divide into three groups of three flags each. The flags are the same for all groups, and represent respectively permission to read the file, “r;” write the file, “w;” or execute the file if it’s an executable, “x.” Write permission also allows the file to be deleted.

The three groups then represent the permissions granted to different classes of users. The first group identifies the permissions granted the owner of the file, and virtually always allows reading and writing. The second flag group gives permissions to other members of the same group of users. In this case, the physics group has read access to the file but not write access. The final flag group gives permissions to the “world,” i.e., all users.

The “x” permission is worth a second look. In Windows, a file with the extension `.exe` is *assumed* to be executable. In Linux, a binary executable is identified by the “x” permission, since we don’t have an explicit file extension to identify it. Furthermore, only those classes of users whose “x” permission is set are allowed to invoke execution of the file. So if I am logged in as an ordinary user, I am not allowed to invoke programs that might change the state of the overall system, such as changing the network address.

Another interesting feature of “x” is that it also applies to shell scripts, which we will come to later in this chapter. For you DOS fans, a shell script is the same thing as a `.bat` file. It is a text file of commands to be executed as a program. But the shell won’t execute the script unless its “x” bit is set.

# The “Root” User

There is one very special user, named “root,” in every Linux system. root can do anything to any file, regardless of the permission flags. Root is primarily intended for system administration purposes, and is not recommended for day-to-day use. Clearly, you can get into a lot of trouble if you are not careful, and root privileges pose a potential security threat. Nevertheless, the kinds of things that embedded and real-time developers do with the system often require write or executable access to files owned by root, and thus require you to be logged in as the root user.

In the past, I would just log in as root most of the time, because it was less hassle. One consequence of this is that every file I created was owned by root, and could not be written by an ordinary user without changing the permissions. It became a vicious circle. The more I logged in as root, the more I had to log in as root to do anything useful. I’ve since adopted the more prudent practice of logging in as a normal user, and only switching to root when necessary.

If you are logged on as a normal user, you can switch to being root with either the `su`, substitute user, or `sudo` commands. The `su` command with no arguments starts up a shell with root privileges, provided you enter the correct root password. To return back to normal user status, terminate the shell by typing `^d` or `exit`.

The `sudo` command allows you to execute a command as root, provided you are properly authorized to do so in the “sudoers file,” `/etc/sudoers`. The sudoers file is, of course, owned by root, so only the root user can authorize sudoers. Once you have been authenticated by entering your own password, you may use `sudo` for a short period of time (default 5 minutes) without reentering your password.

For example, if I wanted to change the permissions on a file in the `/dev` directory, I could execute:

```
    sudo chmod o +rw /dev/tty50
```

I would be prompted for my password and, if entered successfully, the command would be executed. I could then continue to execute `sudo` commands for 5 minutes without having to reenter my password. Note that `sudo` offers better security than `su`, because the root user must authorize sudoers and the root password does not need to be disclosed.

# The /proc File System

The `/proc` file system is an interesting feature of Linux. It acts just like an ordinary file system. You can list the files in the `/proc` directory, you can read and write the files, but they don’t really exist. The information in a `/proc` file is generated on the fly when the file is read. The kernel module that registered a given `/proc` file contains the functions that generate read data and accept write data.

The `/proc` files are a window into the kernel. They provide dynamic information about the state of the system in a way that is easily accessible to user-level tasks and the shell. In the abbreviated directory listing of Fig. 3.9, the directories with number labels represent processes. Each process gets a directory under `/proc`, with several directories and files describing the state of the process.
