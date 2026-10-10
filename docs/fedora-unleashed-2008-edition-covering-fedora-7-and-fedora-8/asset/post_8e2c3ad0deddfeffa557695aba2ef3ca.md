
find, and so saves many command calls. The xargs command automatically places the input at the end of the line, so the previous command might look something like this:

$ xargs chmod o+r file1.txt file2.txt file3.txt

Not every command accepts multiple files, however, and if you specify the -l parameter, xargs executes its command once for each line in its input. If you want to check what it is doing, use the -p parameter to have xargs prompt you before executing each command.

For even more control, the -i parameter enables you to specify exactly where the matching lines should be placed in your command. This is important if you need the lines to appear before the end of the command or need them to appear more than once. Either way, using the -i parameter also enables the -l parameter so that each line is sent to the command individually. This next command finds all files in /home/paul that are larger than 10,000KB in size (10MB) and copies them to /home/paul/archive:

$ find /home/paul -size +10000k | xargs -i cp {} ./home/paul/archive

Using find with xargs is a unique example. All too often, people use pipes when parameters would do the job just as well. For example, these two commands are identical:

$ ps aux --sort=^%cpu | grep -v ‘whoami’

$ ps -N ux --sort=%cpu

The former prints all users and processes and then pipes that to grep, which in turn filters out all lines that contain the output from the program whoami (our username). So, line one prints all processes being run by other users, sorted by CPU use. Line two does not specify the a parameter to ps, which makes it list only our parameters. It then uses the -N parameter to flip that, which means it lists everyone but us, without the need for grep.

The reason people use the former is often just simplicity: Many people know only a handful of parameters to each command, so they can string together two commands simply rather than write one command properly. Unless the command is to be run regularly, this is not a problem. Indeed, the first line would be better because it does not drive people to the manual to find out what ps -N does!

## Multiple Terminals

It is both curious and sad that many Linux veterans have not heard of the screen command. Curious because they needlessly go to extra effort to replicate what screen takes in its stride and sad because they are missing a powerful tool that would benefit them greatly.

Picture this scene: You connect to a server via SSH and are working at the remote shell. You need to open another shell window so that you can have the two running side by side; perhaps you want the output from top in one window while typing in another.

What do you do? Most people would open another SSH connection, but doing so is both wasteful and unnecessary. screen is a terminal multiplexer, which is a fancy term for a program that lets you run multiple terminals inside one terminal.

The best way to learn screen is to try it yourself, so open a console, type screen, and then press Enter. Your display blanks momentarily and then is replaced with a console; it will look like nothing has changed. Now, let’s do something with that terminal. Run top and leave it running for the time being. Hold down the Ctrl key and press a (referred to as Ctrl+a from now on); then let go of them both and press c. Your prompt clears again, leaving you able to type. Run the uptime command.

Pop quiz: What happened to the old terminal running top? It is still running, of course. You can press Ctrl+a and then press 0 (zero) to return to it. Press Ctrl+a and then press 1 to go back to your uptime terminal. While you are viewing other terminals, the commands in the other terminals carry on running as normal so that you can multitask.

Many of screen’s commands are case sensitive, so the lettering used here is very specific: Ctrl+a means “press Ctrl and the a key,” but Ctrl+A means press Ctrl and Shift and the a key¹ so that you get a capital A. Ctrl+a+a means “press Ctrl and the a key, let them go, and then press Shift and the a key.”

You have seen how to create new displays and how to switch between them by number. However, you can also bring up a window list and select windows using your cursor with Ctrl+a+* (that is, press Ctrl and a together, let go, and press the double quotes key [usually Shift and the single quote key]). You will find that the screens you create have the name bash by default, which is not very descriptive. Select a window and press Ctrl+a+A. You are prompted to enter a name for the current window, and your name is used in the window list.

When you get past window 9, it becomes impossible to switch to windows using Ctrl+a and 0-9; as soon as you type the 1 of 10, screen switches to display 1. The solution is to use either the window list or the quick-change option, in which you press Ctrl+a+* (single quote), enter either the screen number or the name you gave it, and then press Enter. You can also change back to the previous window by pressing Ctrl+a+Ctrl+a. If you work within only a small set of windows, you can use Ctrl+a+n and Ctrl+a+p to move to the next and previous windows, respectively. Of course, if you are hanging on to and from windows only to see whether something has changed, you are wasting time (because screen can monitor windows for you and report if anything changes. To enable (or disable) monitoring for a window, use Ctrl+a+M; when something happens, screen flashes a message. If you miss it (the messages disappear when you type something), use Ctrl+a+m to bring up the last message.

password. The second is the most powerful feature of screen: You can exit it and do other things for a while and then reconnect later and screen will pick up where you left off. For example, you could be typing at your desk, disconnect from screen, and then go home, reconnect, and carry on as if nothing had changed. What’s more, all the programs you run from screen carry on running even while screen is disconnected. It even automatically disconnects for you if someone closes your terminal window while it is in a locked state (with Ctrl+a+x).

To disconnect from screen, press Ctrl+a+d. You are returned to the prompt from which you launched screen and can carry on working, close the terminal you had opened, or even log out completely. When you want to reconnect, run the command screen -r. You can, in the meantime, just run screen and start a new session without rescuing the previous one, but that is not wise if you value your sanity! You can disconnect and reconnect the same screen session as many times you want, which potentially means you need never lose your session again.

Although this has a mere taste of screen, we hope you can see how useful it can be.

## Date and Time

The Fedora installer will query you during installation for default time zone settings, and whether your computer’s hardware clock is set to Greenwich mean time (GMT)—more properly known as UTC or coordinated universal time.

Linux provides a system date and time; your computer hardware provides a hardware clock-based time. In many cases, it is possible for the two times to drift apart. Linux system time is based on the number of seconds elapsed since January 1, 1970. Your computer’s hardware time depends on the type of clock chips installed on your PC’s motherboard, and many motherboard chipsets are notoriously subject to drift.

Keeping accurate time is not only important on a single workstation, but also critically important in a network environment. Backups, scheduled downtimes, and other network-wide actions need to be accurately coordinated.

Fedora provides two date and time utilities you can use at the command line:

- **date**—Used to display, set, or adjust the system date and time from the command line
- **hwclock**—A root command to display, set, adjust, and synchronize hardware and system clocks

### Using the date Command

Use the date command to display or set your Linux system time. This command requires you to use a specific sequence of numbers to represent the desired date and time. To see your Linux system’s idea of the current date and time, use the date command like this:

```
$ date
Wed Jan 10 14:17:01 EDT 2005
```
