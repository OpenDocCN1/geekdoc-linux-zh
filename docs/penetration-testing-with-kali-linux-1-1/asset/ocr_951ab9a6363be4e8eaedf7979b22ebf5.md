# 1.8.6.2  Note Taking Tools

There are a number of note taking tools you can choose from such as OneNote<sup>11</sup> (Windows/macOS), DayOne<sup>12</sup> (macOS) or Joplin<sup>13</sup> (MacOS/Windows/Linux) etc. You can also opt to use something like MDwiki,<sup>14</sup> a markdown-based wiki that allows you to write in markdown and then render the output in HTML.

Regardless of your preferred tool, the best way to go about collecting RAW output is to set up some type of logging and forget about it (until it is needed). This way the output is automatically saved and you do not have to worry about remembering to return to your notes. There are a few ways for all output displayed to a terminal to be saved, some of which include:

+   - script: Once executed, all output (including bash's color & backspaces) is saved to a file, which can be replayed at any time.

+   - terminator: An alternate terminal emulator that has various features and plugins, such as Logger (save all output to a text file) and TerminalShot (take a screenshot from within the terminal).

NOTE: Piping the output (>) or using tee is also an option, but you have to use them for each command, so you will have to remember to run them every time.

To deal with the volume of information gathered during a penetration test, we like to use a multipurpose note-taking application to initially document all of our findings. Using such an application helps both in organizing the data digitally as well as mentally. Once the penetration test is over, we can use the interim documentation to compile the full report.

It doesn't matter which program you use for your interim documentation as long as the output is clear and easy-to-read. Get used to documenting your work and findings. It is the only professional way to get the job done!

# 1.8.6.3  Backups

There are two types of people: those who regularly back up their documentation, and those who wish they did. Backups are often thought of as insurance. You never know when you're going to need it until you do! As a general rule, we recommend that you backup your documentation regularly. Keep your backups in a safe place. You certainly don't want them to end up in a public git repo or the cloud!

Documentation should not be the only thing you back up. Make sure you back up important files on your Kali VM, take appropriate snapshots if needed, and so on. It's always best to err on the side of caution.

+   <sup>11</sup> (OneNote, 2019), https://www.onenote.com  
+   <sup>12</sup> (Day One, 2019), http://dayoneapp.com  
+   <sup>13</sup> (laurent22, 2019), https://github.com/laurent22/joplin  
+   <sup>14</sup> (MDwiki, 2019), http://dynalon.github.io/mdwiki/#index.md