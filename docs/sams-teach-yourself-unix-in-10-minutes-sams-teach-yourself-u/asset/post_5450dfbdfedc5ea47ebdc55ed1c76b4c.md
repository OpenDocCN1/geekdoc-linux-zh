
You can also use stty erase Backspace if your keyboard layout makes Backspace more convenient than Delete. If your terminal has gone completely insane and the Return key no longer seems to be working correctly, you can try using the following command: stty sane Ctrl+j. This command attempts to reset the terminal to its default settings, but it isn't guaranteed to work.

## CHANGING KDE's APPEARANCE

Like most desktop environments, KDE includes the capability to customize your desktop environment just as you do under Windows or MacOS. You can set the background, screensaver, fonts, and other attributes of the windowing environment. The changes you make are not system-wide changes; they affect only your personal settings, so feel free to customize to your heart's content! A sample of the different settings that you can customize is shown in Figure 16.1.

![](img/2c005cbaad58c25c7f54da948131a75e_173_0.png)

FIGURE 16.1 KDE offers a wide selection of custom configuration options.

Use the following steps to change KDE's appearance:

- 1. Click the main K toolbar menu item.
- 2. Choose the Settings item from the menu.
- 3. Select the property you want to change (Desktop, Sound, and so on).
- 4. Choose any appropriate sub-property from the category you've chosen. For example, the Desktop enables you to change colors, background, and fonts, among others.
- 5. Make the changes you want, and then click the Apply or OK button to set them.

## SUMMARY

In this lesson, you were introduced to the idea of modifying your environment settings by the use of aliases, Environment Variables, and configuration files. Making these modifications is what enables you to make the environment you work in your own. Following is a review of what was covered in this lesson:

- Environment Variables are frequently used for specifying single configuration options to a program, such as providing a pointer to a directory that the program needs.
- The path variable keeps track of where the system searches for commands when you type them. If a command exists on the system, but the path to the command is not in your path variable, it will not be found when you type the command name.
- Aliases are a very powerful feature of UNIX shells. They enable you to rename commands, or cause commands to always use certain options when you issue them.
- Dot files are everywhere. Many programs use text files containing configuration information for control purposes. These files almost universally have filenames which start with a . character. They are the place to look for automating settings to your shell, and for configuring options for the windowing system.
- The stty command can rescue your terminal session if something has caused it to begin behaving oddly.

Don't be afraid to experiment. You've just made it through a lesson on modifying your user environment. Now go out and do it!

![](img/2c005cbaad58c25c7f54da948131a75e_175_0.png)

## LESSON 17
### PRINTING

*In this lesson you'll learn how you can print requests (or jobs) to a printer on your network.*

As you might be coming to expect, UNIX abstracts the notion of the physical location of the printer, so both local (directly-connected) and remote printers are accessed in the same fashion.

An early divergence in the evolution of UNIX caused there to be two different UNIX printing methodologies: the lp system and the lpd system. lpd was created on the Berkeley Standard Distribution (BSD) UNIX source base, and lp was created on the AT&T System V source base. Unfortunately for the user, these systems are just different enough to make life confusing. From a system administrator's point of view, lp seems to have been created specifically to make life more difficult. Because of this you will find many UNIX machines that are running OS versions based on System V, that have had lp replaced with the BSD lpd system.

## SENDING A PRINT JOB: lpr OR lp

In UNIX, many people can be printing at a single time. Because of this, when you send a print request to a printer it is assigned a job number. If you need to cancel your print job, this number is used to remove the job from the print queue. Only the root user or the person who owns a print job can remove it from the queue.

> **Postscript vs. Non-Postscript** The assumption is made throughout this lesson that you are printing to a Postscript printer. It is possible, however, that your system might be configured to interpret Postscript using a rasterizer, and to print to a non-Postscript printer.

If you're lucky enough to have the lpd system available on your machine, you can use the lpr suite of programs. If you're on a machine that uses lp, watch for the sections pointing out lp differences.

The lpr (line printer) command is the primary method for sending data to the printer. lpr essentially dumps data directly to the printer you specify. To use lpr, follow these steps:

- 1. Determine the name of the printer you want to use. This was probably set by your system administrator.
- 2. Choose the file you want to print. For the moment, only choose a text file. You'll get to see a few other formats shortly.
- 3. Send the print job by using the following command: lpr -P<printer name> <filename> <filename> .... If there is only one printer configured on your computer, chances are you can simply type lpr <filename> <filename> ...

> Be Careful... There's no space between that P and the printer name.

For example, type the following:

```
>lpr -Phod samplefile.txt
```

The result of this command is that the file samplefile.txt is sent to the printer named hod. Depending on the load of the printer, the print job will probably be processed shortly.

> Printing More than One Copy If you need to print multiple copies of a document, you don't need to send separate print jobs. Instead, you can specify the number of copies as an option to the lpr command. Simply follow lpr with #-<number of copies> to print that many copies of each file in the job.

There are a few file formats and special print cases that might require special attention from the print command. This special attention comes in the form of filters that are applied to the file and convert the information into a format that your printer can handle. Following are some filters:

- **.ps** Postscript files. Postscript files will be handled automatically by the lpr command. You can print them as you print a plain text file.
- **.dvi** Tex files. Files from tex contain special page layout instructions. You can use the -d option with lpr in order to print these files correctly.
- **.tr** Troff files. This is the standard file format for man pages. If you want to print out a man page you can use the -t option.
- **Text files with really long lines** If you are having problems printing text files because lines are running off the end of the page, you can have the files reformatted on-the-fly so that they fit. To do this, use -p with lpr.

![](img/2c005cbaad58c25c7f54da948131a75e_177_0.png)

**System Quirks** It's not unusual for a system to be configured without most of the previously mentioned filters installed. You can expect that a conscientious system administrator will have configured your system to handle postscript and plain text properly, but you might find that many have left handling the remainder up to you. In this case you'll have to find and use the appropriate software to process your data files into postscript or plain text, and then send these processed files to the lpr command.

![](img/2c005cbaad58c25c7f54da948131a75e_177_1.png)

**Using lp and lpr** The lp command works much like the lpr command, but with enough differences to make it annoying to the user familiar with lpr. Instead of using a -P option to specify the printer, you use a -d option.

Use -<number of copies> instead of -#<number of copies>.

When you send a job to the printer with lp, it gives you a message such as the following: request id is <uniqname> #. Remember this <uniqname> # combination because that's what you'll need to know to remove the job if you decide you don't want it to print after all.

The lp system is supposed to make your life easier by handling detection of file types and appropriate conversions automatically, instead of specific options for specific types of files, however, every type of printer and every installation can have different options available. Hopefully, you will never need to know these installation-specific options, but if you do, check your local documentation to find out what your system can do.

## CHECKING THE STATUS OF A PRINT JOB: lpq

After you've sent a job to the printer, chances are you'll want to be able to check to see if it is done printing especially if it is a network printer located on another floor in your building or in another building altogether! To check the status of a job, you'll want to look at the queue for the printer to which you submitted the job. You do this with the lpq -p<printer name> command. Once again, if there is only a single printer on your system, you can probably just issue lpq by itself.

For example, type the following:

```
>lpq -Phod
```

| Rank | Owner | Job | Files | Total Size |
|---|---|---|---|---|
| 1st | agrove | 27 | test.txt | 19 bytes |
| 2nd | jray | 28 | samplefile.txt | 10021 bytes |

This example shows that there are currently two different jobs in the printer queue for hod. One is owned by agrove, and the user jray owns
