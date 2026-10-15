
## 2.2.1 Creating the Script

Step one would be to create a directory for storing and testing the scripts to be created (see Listing 2.2). Depending on your needs, creating a tree of directories for your different projects would be a good idea. Again, you don’t have to follow these examples verbatim; just create something that is usable for you and reflects your train of thought. Remember, though, a directory tree containing all the valuable work is easier to back up than countless directories scattered all over the hard disk. See Chapter 4 for scripts to automate the process.

![](img/e121d664a879353483b8ef78e54b87ea_43_0.png)

> One word of advice—use a "normal" account for development work, unless it is absolutely necessary to switch to superuser. An account with restricted rights on the system prevents possible damage to it. Some commands have destructive side effects, and it is better to get an error message than to re-install the whole system. Programs with the potential to take the computer down should be tested on a test system, which resembles the target platform as close as possible. If the test system needs to be reinstalled, it is a lesson learned; if a production server needs to be reinstalled, that’s a far more serious matter.

### LISTING 2.2 A Directory Structure for Development 1

```
erikk@unixhost:~> mkdir -p work/df_check
erikk@unixhost:~> ls -lR work
work:
total 2
drwxr-xr-x  2 erikk  staff      512 Jun 29 10:49 df_check

work/df_check:
total 0
```

The structure shown in Listing 2.2 is rather simplistic. There is a directory called work, which contains a directory named df_check. Depending on the needs, this structure could be sufficient. A more structured approach is shown in Listing 2.3.

### LISTING 2.3 Directory Structure for Development 2

```
erikk@unixhost:~> mkdir -p work/df_check/RCs work/df_check/doc
erikk@unixhost:~> touch work/df_check/ToDo.txt
erikk@unixhost:~> ls -lR work
work:
total 2
drwxr-xr-x  4 erikk  staff       512 Jun 29 11:29 df_check

work/df_check:
 total 6
drwxr-xr-x  2 erikk  staff       512 Jun 29 11:05 RCS
-rw-r--r--  1 erikk  staff         0 Jun 29 11:29 ToDo.txt
drwxr-xr-x  2 erikk  staff       512 Jun 29 11:05 doc

work/df_check/RCS:
 total 0

work/df_check/doc:
 total 0
```

Now there are two more directories, doc to hold the documentation if necessary and RCS for version control. We’ll talk more about versioning later. The file ToDo.txt will be used as a scratch pad of things to be taken care of at a later time (the reason to use a capital T in the filename is simple; because the files are sorted alphabetically, if you use a capital letters, those files will show up on top of a listing created by ls).

## Choose an Editor

Which text editor should you use? There is a simple answer: the one you feel comfortable with. A more complex answer would be as follows: the right tool for the job at hand that you feel comfortable with. *NIX, as always, puts you into the position to choose from more than one alternative. The more common choices would be vi or emacs, followed by a dozen other programs. Depending on who you ask, you’ll be swamped with reasons why the favorite editor of the person asked is the best choice.

The question about the best editor can spark a lively discussion among programmers and system administrators. Simply try to imagine a group of physicists confronted with the sentence “It is possible to travel faster than light!” Their inevitable reaction is nothing compared to the vehemence with which people defend their editor.

We’re using both vi and emacs for reasons that probably don’t apply to you: vi is available on every *NIX-based system. If you are not a hundred percent sure emacs, or whatever editor you have chosen for life, is available on every system you are responsible for, try to at least maintain a certain knowledge of vi. You will need it in due time.

This book was written with emacs.
If your time permits, try to experiment with as many editors as you like and choose the best candidate. Just make sure your choice is available on every system you administer, regardless of operational status. And if you should be bored at a *NIX-related conference, mention your editor of choice.

Now, the file ToDo.txt will be put under version control, although it is not absolutely necessary. The file needs the contents shown in Listing 2.4 to enable versioning.

### LISTING 2.4 Contents of ToDo.txt

```
erikk@unixhost:~> head ToDo.txt
$Id$
- read in output of 'df -h' and process it
```

ToDo.txt is a simple text file, apart from the odd-looking first line. $Id$ is used for version control; when checked in, it will be replaced with the version number and some other information. Although this first line is not a necessity to make use of version control, it allows the user to recognize the fact that it was put under version control and displays the current version. The necessary steps to put the file under version control are shown in Listing 2.5.

### LISTING 2.5 Putting ToDo.txt under Version Control

```
erikk@unixhost:~> ci -l ToDo.txt
RCS/ToDo.txt,v <-- ToDo.txt
enter description, terminated with single '.' or end of file:
NOTE: This is NOT the log message!
>> start
>> . initial revision: 1.1
done
erikk@unixhost:~> head ToDo.txt
$Id: ToDo.txt,v 1.1 2004/06/29 09:44:31 erikk Exp erikk $
- read in output of 'df -h' and process it
erikk@unixhost:~> ls -l RCS
total 2
-r--r--r-- 1 erikk staff 245 Jun 29 11:44 ToDo.txt,v
```

The command ci -l ToDo.txt puts the file under version control. ci is a moniker for "check in." The option -l tells ci to "lock" the file and keep it where it
