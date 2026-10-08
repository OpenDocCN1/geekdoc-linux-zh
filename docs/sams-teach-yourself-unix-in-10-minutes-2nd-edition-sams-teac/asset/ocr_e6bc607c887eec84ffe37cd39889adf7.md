# Summary

Reading files in your Unix system can be done very easily. Working via the command prompt can be difficult but by now, that difficulty level should be diminishing and fading away as you learn more and more about Unix. In this lesson we learned how to work with Unix files and read them via many shell prompt tools. This lesson should have given you a clear picture of the many different ways you can display files, or portions of files.

Here’s a review:

+   **cat**—This concatenate command displays all the files you specify, one after the other. It does not pause at the end of pages.

+   **more/less**—These are known as pagers. They page through their input files, one you’re trying to look at header information. less offers the ability to scroll backwards through files unlike more. more provides forward-only viewing.

+   **head**—Displays the first few lines of a file. This is useful when you’re trying to look at header information in files such as email messages.

+   **tail**—Views the end of a file. Used with the -f option, tail provides the useful capability of displaying a logfile as it is generated. Rather than each program needing its own monitoring utility, tail -f can be used.

+   **Other file formats**—Although many Unix information files are text or HTML based, there are other formats that you might encounter. This lesson looked briefly at some of those formats, and the programs that you can use to work with them.