# chsh: changes your login shell

tip The person who sets up your account determines which shell you will use when you first log in on the system or when you open a terminal emulator window in a GUI environment. You can run any shell you like once you are logged in. Enter the name of the shell you want to use (*bash*, *tcsh*, or another shell) and press RETURN; the next prompt will be that of the new shell. Give an *exit* command to return to the previous shell. Because shells you call in this manner are nested (one runs on top of the other), you will be able to log out only from your original shell. When you have nested several shells, keep giving *exit* commands until you reach your original shell. You will then be able to log out.

Use the *chsh* utility when you want to change your login shell permanently. First give the command *chsh*. Then in response to the prompts enter your password and the absolute pathname of the shell you want to use (*/*bin/*bash*, /*bin/*tcsh*, or the pathname of another shell). When you change your login shell in this manner using a terminal emulator (page 118) under a GUI, subsequent terminal emulator windows will not reflect the change until you log out of the system and log back in.

# THE KEYBOARD AND SCREEN AS STANDARD INPUT AND STANDARD OUTPUT

When you first log in, the shell directs standard output of your commands to the device file that represents your screen (Figure 7-4). Directing output in this manner causes it to appear on your screen. The shell also directs standard input to come from the same file, so that your commands receive as input anything you type on the keyboard.

cat The *cat* utility provides a good example of the way the keyboard and the screen function as standard input and standard output, respectively. When you use *cat*, it copies a file to standard output. Because the shell directs standard output to the screen, *cat* displays the file on the screen.

![](bbox=[0.45, 0.68, 0.7, 0.84])

**Figure 7-4** By default, standard input comes from the keyboard and standard output goes to the screen