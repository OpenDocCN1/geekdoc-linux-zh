The easiest way to troubleshoot logical control statements (if, which, while, and so on) inside scripts is to uncomment them out (as shown in the following example) so the lines of script inside their control will execute automatically:

```
if (dog = 2)
{
    echo 'the value of dog is two'
}
fi
now to debug this change the code to the following,
# if (dog = 2)
# {
    echo 'the value of dog is two'
#}
# fi
```

With larger shell scripts, selective commenting and uncommenting will be needed. It would be rather tedious to comment out five thousand lines of code and then uncomment the same lines of code when you are finished. So clearly, this power technique of selectively commenting out blocks of code to see what happens is really only practical with smaller scripts.

Another common problem with a shell script is when the shell script either tries to call a nonexistent command or tries to call a command in a directory without the user's permissions. Check to make sure the called files exist and are accessible from the script.

The developers of professionally produced software will give system administrators the names of the processes that are associated with their programs. You can use the line `ps -ef | grep` command to show if a process is running.

Developers typically also include log files with their programs. These text files have various error messages that relate to the running of the application. Another common technique is to include a README file with the program. The README file will have information that did not make it into the user's guide and the system administrator's guide.

# Summary

This chapter explained some of the methods that you can use to troubleshoot a Solaris workstation or server. You can make the process easier to deal with by documenting your equipment and software prior to encountering difficulties. An essential practice in escaping problems that can't be solved is to make sure that you have a