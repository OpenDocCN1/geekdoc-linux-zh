means

```
[wh11@freedom /home/wh11]$ 
```

If you're in the "zips" subdirectory of your home directory (for example, /home/wh11/zips), you'd see this:

```
[wh11@freedom zips]$ 
```

# 3. Command prompts for root vs. regular user

The prompt ends in either a dollar sign ($) or a pound sign (#). The $ means that you are logged on as a regular user. The # means you are logged on as root. You'll hear this again, but note that if you're logged on as root in a command window, you can easily mangle or destroy your system with one typographic error.

# 4. Customize your prompt

You can customize the prompt by making changes to certain configuration files.

The behavior of the command window (more specifically, the behavior of the shell) depends on values in several configuration files. Linux looks at the /etc/profile file first, then the ~/.bash_profile file, and then the ~/.bashrc file. (If you're using a different shell, these files are different.)

The first file is a generic, system-wide file that runs regardless of which user is logging on, and only the system administrator can modify this file. As you can see, there is a copy of the second file in every user's home directory, and it runs every time that user logs in. Because each user has her own ~/.bash_profile file, the command window can be customized on a per-user basis.

The third file, which also exists in every user's home directory, also runs on a user-by-user basis whenever a new command window is opened, except during initial login. As a result of having separate .bash_profile and .bashrc files, each user can run specific customizations just during initial login or for all command windows except during initial login. You might be thinking that while this complex mechanism makes for wonderful flexibility, it's also awkward if you want to run some customizations for a specific user, but also for every command window, because you'd have to add the same customizations to both files. Ha! Gotech covered that: Fedora Core's default .bash_profile file comes with a short script that looks like this:

```
# Get the aliases and functions
if [ -f ~/.bashrc ]; then
. ~/.bashrc
fi
```

Don't worry about how it works; the important thing is that this script makes bash run the .bashrc file in the user's home directory whenever the .bash_profile script runs. As a result, if you put all of your customizations in .bashrc, they'll run for every shell. But you still need customizations that run only during login, put them before this line in .bash_profile.

It's a good idea to put anything that takes a noticeable amount of time in .bash_profile so that subshells start up really fast by doing only the minimum in .bashrc.

And, of course, this all applies to the root user as well as every other user. The root user's .bash_profile and .bashrc files are in /root, of course.