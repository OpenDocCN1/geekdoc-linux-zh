
## Multiple Terminals

It is both curious and sad that many Linux veterans have not heard of the screen command. Curious because they needlessly go to extra effort to replicate what screen takes in its stride and sad because they are missing a powerful tool that would benefit them greatly.

Picture this scene: You connect to a server via SSH and are working at the remote shell. You need to open another shell window so you can have the two running side by side; perhaps you want the output from top in one window while typing in another. What do you do? Most people would open another SSH connection, but that is both wasteful and unnecessary. screen is a terminal multiplexer, which is a fancy term for a program that lets you run multiple terminals inside one terminal.

The best way to learn screen is to try it yourself, so open a console, type screen, and then press Enter. Your display will blank momentarily and then be replaced with a console; it will look like nothing has changed. Now, let’s do something with that terminal. Run top and leave it running for the time being. Hold down the Ctrl key and press a (referred to as Ctrl+a from now on); then let go of them both and press c. Your prompt will again, leaving you able to type. Run the uptime command.

Pop quiz: What happened to the old terminal running top? It is still running, of course. You can type Ctrl+a and then press 0 to return to it. Type Ctrl+a and then press 1 to go back to your uptime terminal. While you are viewing other terminals, the commands in the other terminals carry on running as normal so you can multitask.

Many of screen’s commands are case sensitive, so the lettering used here is very specific: Ctrl+a means “press Ctrl and the a key,” but Ctrl+A means “press Ctrl and Shift and the a key” so you get a capital A. Ctrl+aA means “press Ctrl and the a key, let them go, and then press Shift and the a key.”

You have seen how to create new displays and how to switch between them by number. However, you can also bring up a window list and select windows using your cursor with Ctrl+a" (that is, press Ctrl and a together, let go, and press the double quotes key [usually Shift and the single quote key]). You will find that the screens you create have the name bash by default, which is not very descriptive. Select a window and press Ctrl+aA. You are prompted to enter a name for the current window, and your name is used in the window list.

Once you get past window 9, it becomes impossible to switch to windows using Ctrl+a and 0-9; as soon as you type the 1 of 10, screen switches to display 1. The solution is to use either the window list or the quick change option, in which you press Ctrl+a’ (single quote), enter either the screen number or the name you gave it, then press Enter. You can also change back to the previous window by pressing Ctrl+aCtrl+a. If you only work within a small set of windows, you can use Ctrl+aN and Ctrl+aP to move to the next and previous windows, respectively. Of course, if you are changing to and from windows only to see whether something has changed, you are wasting time because screen can monitor windows for you and report if anything changes. To enable (or disable) monitoring for a window, use Ctrl+a+M; when something happens, screen flashes a message. If you miss it (the messages disappear when you type something), use Ctrl+a+m to bring up the last message.

Windows close when you kill the main program inside. Using Ctrl+a+c, this window is Bash; type exit to quit. Alternatively, you can use Ctrl+a+k to kill a window. When all your windows are closed, screen terminates and prints a screen is terminating message so you know you are out.

However, there are two alternatives to quitting: locking and disconnecting. The first, activated with Ctrl+a+x, locks access to your screen data until you enter your system password. The second is the most powerful feature of screen: you can exit it and do other things for a while and then reconnect later and screen will pick up where you left off. For example, you could be typing at your desk, disconnect from screen, then go home, reconnect, and carry on as if nothing had changed. What’s more, all the programs you ran from screen carry on running even while screen is disconnected. It even automatically disconnects for you if someone closes your terminal window while it is in a locked state (with Ctrl+a+x).

To disconnect from screen, press Ctrl+a+d. You are returned to the prompt from which you launched screen and can carry on working, close the terminal you had opened, or even log out completely. When you want to reconnect, run the command screen -r. You can, in the meantime, just run screen and start a new session without resuming the previous one, but that is not wise if you value your sanity! You can disconnect and reconnect the same screen session as many times as you want, which potentially means you need never lose your session again.

Although this has been a mere taster of screen, hopefully you can see how useful it can be.

## Reference

- http://www.gnu.org/—The website of the GNU project, it contains manuals and downloads for lots of command-line software.
- http://www.linuxdevcenter.com/linux/cmd/—A wide selection of Linux commands and explanations of what they do.
- http://www.tuxfiles.org/linuxhelp/cli.html—Several short command-line tutorials, courtesy of tuxFiles.
- http://www.linuxcommand.org/—Describes itself as “your one-stop command line shop!” It contains a wealth of useful information about the console.

## Books

Understanding the way UNIX works at the nuts and bolts level can be both challenging and rewarding, and there are several good books that will help guide you on your way.
