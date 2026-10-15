
## Task 3.5: PATH and HOME

The two most important values in your environment are the name of your home directory (HOME) and your search path (PATH). Your home directory (as it’s known) is the name of the directory in which you always begin your Unix session.

The PATH environment variable lists the set of directories, in left-to-right order, that the system searches to find commands and applications you request. You can see from the example that my search path tells the computer to start looking in the /home/taylor/bin directory, and then sequentially try /bin, /usr/bin, /usr/ucb, /usr/local/bin, /usr/unsup/bin, and . before concluding that it can’t find the requested command. Without a PATH, the shell wouldn’t be able to find any of the many, many Unix commands. At a minimum, you always should have /bin and /usr/bin.

- 1. You can use the echo command to list specific environment variables, too. Enter echo $PATH and echo $HOME. If you forget the $, then the shell doesn’t know you are specifying that you want to know the value of the named variable. Try it; you’ll see what I mean.
- 
- When I enter the two echo statements as shown above, I get the following results:

Click here to view code image

```
% echo $PATH
/home/taylor/bin:/bin:/usr/bin:/usr/ucb:/usr/local/bin:/usr/unsup/bin:.
% echo $HOME
/home/taylor
%
```

- 2. Your PATH value is probably similar, although certainly not identical, to mine, and your HOME is /home/accountname or something similar (where accountname is your account name).

Try it for yourself. Any surprises in your PATH?

## Task 3.6: Find Where You Are with pwd

So far you’ve learned a lot about how the file system works but not much about how to move around in the file system. With any trip, the first and most important step is to find out your current location—that is, the directory in which you are currently working. In Unix, the command pwd tells you the present working directory.

- 1. Enter pwd:

```
% echo $HOME
/home/taylor
% pwd
/home/taylor
%
```

The output should be identical to the output you saw when you entered env HOME because you’re still in your home directory.

Think of pwd as a compass that’s always capable of telling you where you are. It also tells you the names of all directories above you because it always lists your current location as an absolute directory name.

## Task 3.7: Moving to Another Location with cd

The other half of the dynamic duo is the cd command, which is used to change directories. The format of this command is simple, too: cd new-directory (where new-directory is the name of the new directory you want).

- 1. Try moving to the very top level of the file system and entering pwd to see whether the computer agrees that you’ve moved:
  % cd /
  % pwd
  /
  %

- 2. Notice that cd doesn’t produce any output. Many Unix commands operate silently like this, unless an error is encountered. The system then indicates the problem. You can see what an error looks like by trying to change your location to a nonexistent directory. Try the /taylor directory to see what happens:

Click here to view code image

```
% cd /taylor
/taylor: No such file or directory
%
```

- 3. Enter cd without specifying a directory. What happens? I get the following result:
  % cd
  % pwd
  /home/taylor
  %

- 4. Here’s where the HOME environment variable comes into play. Without any directory specified, cd moves you back to your home directory automatically. If you get lost, it’s a fast shorthand way to move to a known location without fuss.
  Remember the dot-dot notation for moving up a level in the directory hierarchy? Here’s where it also proves exceptionally useful. Use the cd command without any arguments to move to your home directory, and then use pwd to ensure that’s where you’ve ended up.

- 5. Now, move up one level by using cd .. and check the results with pwd:
  % cd
  % pwd
  /home/taylor
  % cd ..
  % pwd
  /home
  %

- 6. Use the ls -C -F command to list all the directories contained at this point in the file system:
