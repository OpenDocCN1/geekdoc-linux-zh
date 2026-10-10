```
```
echo This script name is $0.
exit
$ bash positional0.sh
This script name is positional0.sh.
$ ```,

```

However, there is a potential problem. When using a different command to run the shell script, the command becomes entangled with the script name in the $0 parameter:

```
```
$ ./positional0.sh
This script name is ./positional0.sh.
$ ```,

```

An additional issue occurs when the actual string passed is the full script path, and not just the script's name. In this case, the $0 variable gets set to the full script path and name:

```
```
$ SHOME/scripts/positional0.sh
This script name is /home/christine/scripts/positional0.sh.
$ ```,

```

If you want to write a script that only uses the script's name, you'll have to do a little work in order to strip off whatever path is used to run the script or any entangled commands. Fortunately, there's a handy little command available that does just that. The basename command returns just the script's name without the path:

```
```
$ cat posbasename.sh
#!/bin/bash
# Using basename with the $0 command-line parameter
# 
name=$(basename $0)
# 
echo This script name is $name.
exit
$ ./posbasename.sh
This script name is posbasename.sh.
$ ```,

```

Now that's much better. You can use this technique to write a script that produces log messages identifying when it ran:

```
```
$ cat checksystem.sh ```,

```