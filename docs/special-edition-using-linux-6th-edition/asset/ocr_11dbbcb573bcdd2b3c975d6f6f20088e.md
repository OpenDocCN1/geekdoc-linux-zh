*When I try to execute a file, I get permission denied. It’s a shell script, and I can read the file, so why can’t I execute it?*

The shell script you’re trying to run probably does not have the execute bit set for you. If you own the file, you must set the owner execute bit (`chmod u+x`). If you are in the group, you must set the group execute bit (`chmod g+s`). Otherwise, you must set the world execute bit (`chmod o+x`). If this still doesn’t fix your problem, your filesystem is not mounted exec—see next question.

*I have a CD-ROM with a file `install.sh`. The CD-ROM is mounted, but I can’t execute the file with `./install.sh`. I get an error message: permission denied. I can read the file okay, and the file has the execute bit set. What’s wrong?*

In `/etc/fstab`, you have the mount line with `user` in it, but you don’t have `exec` after the user listing (it must follow `user`). If you can’t change this line and remount the CD-ROM, run the file this way: `sh ./install.sh`.

*As root, I try to delete a file, but I can’t. Instead, I get an error message.*

More than likely, either the ext2 immutable bit or the append bit has been set on this file. Try `chattr -ia <filename>`, which will turn off the immutable and append bits. You should then be able to delete the file.