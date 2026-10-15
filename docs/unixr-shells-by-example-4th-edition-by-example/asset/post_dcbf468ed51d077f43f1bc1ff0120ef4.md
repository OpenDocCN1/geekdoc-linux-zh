
### EXAMPLE 10.46 (CONTINUED)

(The Output)

```text
Hello, in 1st loop
In 2nd loop
In 3rd loop
Out of all loops
```

#### EXPLANATION

- 1. Start the first while loop.
- 2. Enter the second nested while loop.
- 3. Enter the third nested while loop.
- 4. The repeat command will cause break to be executed three times; it will break first out of this innermost loop, then the second loop, and last, the first loop. Control continues at line 5.
- 5. Program control starts here after loop terminates.

The continue Command. The continue statement starts execution at the top of the innermost loop.

### EXAMPLE 10.47

```
1 set done = 0
2 while ( ! $done )
    echo "Are you finished yet?"
    set answer = $<
3   if ("$answer" =~ [Nn]*) continue
4   set done = 1
5 end
```

#### EXPLANATION

- 1. The variable done is assigned 0.
- 2. The expression is tested. It reads: while (! 0). Not 0 is evaluated as true (logical NOT).
- 3. If the user entered No, no, or nope (anything starting with N or n), the expression is true and the continue statement returns control to the top of the loop where the expression is re-evaluated.
- 4. If answer does not start with N or n, the variable done is reset to one. When the end of the loop is reached, control starts at the top of the loop and the expression is tested. It reads: while (! 1). Not 1 is false. The loop exits.
- 5. This marks the end of the while loop.

### EXAMPLE 10.48

(The Script)

```sh
#!/bin/csh
1  if ( ! -e memo ) then
echo "memo file non existent"
exit 1
endif
2  foreach person (anish bob don karl jaye)
3    if ($person == [Kk]arl) continue
4  mail -s "Party time" $person < memo
end
```

#### EXPLANATION

- 1. A file check is done. If the file memo does not exist, the user is sent an error message and the program exits with a status of 1.
- 2. The loop will assign each person in the list to the variable person, in turn, and then shift off the name in the list to process the next one.
- 3. If the person's name is Karl or karl, the continue statement starts execution at the top of the foreach loop (Karl is not sent the memo because his name was shifted off after being assigned to person.) The next name in the list is assigned to person.
- 4. Everyone on the mailing list is sent the memo, except karl.

## 10.8 Interrupt Handling

If a script is interrupted with the Interrupt key, it terminates and control is returned to the C shell; that is, you get your prompt back. The onintr command is used to process interrupts within a script. It allows you to either ignore the interrupt (^C) or transfer control to another part of the program before exiting. Normally, the interrupt command is used with a label to "clean up" before exiting. The onintr command without arguments restores the default action.

### EXAMPLE 10.49

(The Script)

```sh
1  onintr finish
2  < Script continues here >
3  finish:
4  onintr -	# Disable further interrupts
5  echo Cleaning temp files
6  rm $$tmp*; exit 1
```

#### EXPLANATION

- 1. The `onintr` command is followed by a label name. The label finish is a user-defined label; control will be transferred to the label if an interrupt occurs. Usually this line is at the beginning of the script. It is not in effect until it is executed in the script.
- 2. The rest of the script lines are executed unless `^C` (Interrupt key) is pressed while the program is in execution, at which time, control is transferred to the label.
- 3. This is the label; when the interrupt comes in, the program will continue to run, executing the statements below the label.
- 4. To shield this part of the script from further interrupts, the `onintr -` is used. If `^C` is entered now, it will be ignored.
- 5. This line is echoed to the screen.
- 6. All tmp files are removed. The tmp files are prefixed with the shell's PID (`$$`) number and suffixed with any number of characters. The program exits with a status of 1.

## 10.9 setuid Scripts

Whoever runs a setuid program temporarily (as long as he or she is running the setuid program) becomes the owner of that program and has the same permissions as the owner. The passwd program is a good example of a setuid program. When you change your password, you temporarily become root, but only during the execution of the passwd program. That is why you are able to change your password in the /etc/passwd (or /etc/shadow) file, which normally is off-limits to regular users.

Shell programs can be written as setuid programs. You might want to do this if you have a script that is accessing a file containing information that should not be accessible to regular users, such as salary or other personal information. If the script is a setuid script, the person running the script can have access to the data, but it is still restricted from others. A setuid program requires the following steps:

- 1. In the script, the first line is

   ```sh
   #!/bin/csh -feb
   ```

   where the `-feb` options are

   ```text
   -f  fast start up; don't execute .cshrc
   -e  abort immediately if interrupted
   -b  this is a setuid script
   ```

- 2. Next, change the permissions on the script so that it can run as a setuid program:

   ```sh
   % chmod 4755 script_name
   or
   % chmod +srx script_name
   % ls -l
   -rwsr-xr-x  2 ellie       512 Oct 10 17:18 script_name
   ```
