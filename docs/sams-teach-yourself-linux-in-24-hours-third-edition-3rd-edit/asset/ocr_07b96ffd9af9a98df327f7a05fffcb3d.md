This makes it possible to reduce complex jobs that require many command steps into a simple matter of typing one command (and maybe adding little information) to have the shell take care of the whole thing for you.

# New TERM

Simply put, a shell script is a list of actions that you want the shell to perform that includes the order in which you want the actions performed and where you want the expected results sent.

The basic command philosophy of UNIX, and therefore Linux, is to provide the user with myriad small and specialized commands that can be “plumbed” together with conditional statements, command redirection, and pipes to produce a desired outcome. Your first step in writing a script is to open a text editor (which you’ll learn more about in Hour 8, “Text Editing with vi”) and start stringing commands together. The combination of commands and conditional statements might produce a script such as

```
if cp "filename1" "filename2"
then
  vi "filename2"
else
  echo "failed to make copy"
fi
```

This command string tells bash to copy filename1 to filename2, and then call the vi text editor with filename2 displayed. If bash cannot copy the file, the then statement cannot be met and bash cannot open vi with the file. The else statement then directs bash to print the message ‘failed to make copy’ (without the quotes). The final fi is the finish statement and must be present for if...then...else statements to work. Omitting this is a common error and is the cause of many script failures.

After you have written your script, save the file and make it an executable script by using the chmod command as shown here:

```
chmod +x [filename]
```

Any short name you choose to call the script will become the command that you type to run the shell script.

![](bbox=[0.2, 0.9, 0.3, 0.97])

> You’ll learn more about writing scripts in Hour 17, “Automating System Administration Tasks.”