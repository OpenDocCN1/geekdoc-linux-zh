6. In the for loop, right after the do line, before the first echo command, insert the following lines to turn on shell tracing only for file names starting with w:

```
case $i in
  w*) set -x ;;
  *) set +x ;;
esac
```

7. Save your file and exit the text editor.

8. Test the syntax of your script. You should see no output:

```
bash -n ./fileinfo
```

9. Now you can run the script without using the -x option on the command line, because you are setting the shell trace feature inside the script. Try this command:

```
./fileinfo /etc/[msw]*conf > scripts save
```

You see no shell tracing output, though you thought you had set up the script to turn it on for file names starting with w.

10. After some head scratching, you realize that the file names you are using all start with /etc/—the script doesn’t know that you mean the file name without any path before it. You could add commands to strip that information off, but you choose to take an easier approach for now. First, change to the /etc directory, so you can refer to the configuration files without including /etc/ in front of the file names:

```
cd /etc
```

11. Now execute the script in your home directory:

```
~/fileinfo [msw]*conf > ~/scripts save
```

You see on the screen shell tracing output only for file names that begin with “w”. The rest of the script output is stored in your home directory in the scripts save file.

12. Exit the command-line window and log off.