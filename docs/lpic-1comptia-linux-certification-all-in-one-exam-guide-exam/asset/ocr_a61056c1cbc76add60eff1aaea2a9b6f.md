+   f. Enter `exit` twice to close the second terminal window.

+   g. Switch to the terminal session where `tail` is running and press `CTRL-C` to break out of `tail`.

+   11. Switch back to your regular user account by entering `exit`.

+   12. Delete the `MyFiles` directory in your home directory by entering `rm -r ~/MyFiles`.

+   13. Enter `ls` and verify that the directory and its contents are gone.

+   14. Make a copy of your home directory files and subdirectories in `/tmp` by entering `cp -R ~/ /tmp/`.

+   15. View the contents of `/tmp` by entering `ls /tmp/`. Verify that your home directory was copied.

+   16. Work with symbolic links by doing the following:

+   a. Create a symbolic link from a directory named `docs` in your home directory to the `/usr/share/doc` directory by entering `ln -s /usr/share/doc/ ~/docs`.

+   b. Enter `ls -l`. Verify that the `docs` file points to `/usr/share/doc/`.

+   c. Enter `cd docs`.

+   d. Enter `pwd`. What directory are you in?

+   e. Enter `ls`. You should see the contents of the `/usr/share/doc/` directory even though you are still in `~/docs`.

# ## Finding Content Within Files

Earlier in this chapter, we discussed shell commands that can be used to search for files in the file system. However, Linux also provides a utility called `grep` that you can use to search for specific content *within* a file. The `grep` utility is extremely useful; in fact, I dare say that most Linux admins use it on a daily basis. Using `grep`, you can search through a file for a particular text string. This can come in handy when you want to search a very large log file for a specific message or when you need to find a specific directive within a configuration file. You can even use `grep` to search through multiple files at once to locate a particular expression.

To use `grep`, you enter `grep search_expression file_name` at the shell prompt. For example, let’s suppose you want to search through your `/var/log/messages` file for any log entries related to the VNC service running on your Linux system. You would enter `grep vnc /var/log/messages`. The `grep` utility would then display each line from the file that contained your search term, as shown here:

```
```text
fs2:~ # grep vnc /var/log/messages
Feb 1 13:47:25 fs2 xinetd[7134]: Reading included configuration file:
/etc/xinetd.d/vnc [file=/etc/xinetd.d/vnc] [line=15]
fs2:~ #
```
```