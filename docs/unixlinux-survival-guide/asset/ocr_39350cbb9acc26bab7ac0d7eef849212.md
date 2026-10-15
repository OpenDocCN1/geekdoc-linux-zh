is; otherwise, it would create the file TODO.txt,v in the directory RCS and delete the original. To get it back, you would have to execute the command co TODO.txt.

The latter approach is fine while working with a team of programmers or fellow system administrators, but for the purpose of developing for yourself, it is easier to keep the files handy. The moment the file is "unlocked," it becomes writable for other programmers, provided they have access to the RCS directory (if one of those programmers chooses to work with the file, the file is properly locked again while that programmer works on it). This mechanism allows multiple programmers to work on the same files without overwriting changes introduced by others. If one is not able to obtain a lock on a file, that file is usually locked by another programmer for editing.

As shown in Listing 2.5, the string $Id$ is replaced with $Id: To-Do.txt,v 1.1 2004/06/29 09:44:31 erikk Exp erikk $. It contains the name of the RCS file, the current version number, 1.1, the date it was checked in last, and the username of the person executing the check-in.

Now you are ready to start the creation of the script. Insert the contents shown in Listing 2.6 into the file df_check.sh. Using an extension to the filename is not a real requirement in *NIX, but it can help you remember which interpreter is used to execute the file.

# LISTING 2.6 Creating the First Version of the Script df_check.sh

```
#!/bin/sh
#
# $Id$
################################################################
#
#       file:          df_check.sh
#
#       purpose:       script to monitor the status
#                      of mounted volumes
#
#       author:        Erik Keller
#
#       parameters:
#
################################################################

df -h

# EOF
```