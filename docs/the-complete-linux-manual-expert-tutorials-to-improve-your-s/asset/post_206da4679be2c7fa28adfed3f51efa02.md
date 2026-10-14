
## Creating Bash Scripts
— Part 4

You’ve encountered user interaction with your scripts, asking what the user’s name is and so on. You’ve also looked at creating loops within the script to either count or simply do something several times. Let’s combine and expand some more.

## CHOICES AND LOOPS

Let’s bring in another command, CHOICE, along with some nested IF and ELSE statements. Start by creating a new script called mychoice.sh.

### STEP 1

The mychoice.sh script is beginning to look a lot more complex. What we have here is a list of four choices, with three possible options. The options: Mint, Is, and Awesome will be displayed if the user presses the correct option key. If not, then the menu will reappear, the fourth choice.

![](img/f80199d101da92d953f18eaa6205b48e_73_0.png)

### STEP 3

You can, of course, increase the number of choices but you need to make sure that you match the number of choices to the number of IF statements. The script can quickly become a very busy screen to look at. This lengthy script is another way of displaying a menu, this time with a fancy colour scheme too.

![](img/f80199d101da92d953f18eaa6205b48e_73_1.png)

### STEP 2

If you follow the script through you soon get the hang of what’s going on, based on what we’ve already covered. WHILE, IF, and ELSE, with the FI closing loop statement will run through the options and bring you back to the start if you pick the wrong option.

![](img/f80199d101da92d953f18eaa6205b48e_73_2.png)

### STEP 4

You can use the arrow keys and Enter in the menu setup in the script. Each choice is an external command that feeds back various information. Play around with the commands and choices, and see what you can come up with. It’s a bit beyond what we’ve looked at but it gives a good idea of what can be achieved.

![](img/f80199d101da92d953f18eaa6205b48e_73_3.png)

## CREATING A BACKUP TASK SCRIPT

One of the most well used examples of Bash scripting is the creation of a backup routine, one that automates the task as well as adding some customisations along the way.

### STEP 1

A very basic backup script would look something along the lines of: #!/bin/bash, then, tar cvfz ~/backups/my-backup.tgz ~/Documents/. This will create a compressed file backup of the ~/Documents folder with everything in it, and put it in a folder called /backups with the name my-backup.tgz.

### STEP 2

While perfectly fine, we can make the simple script a lot more interactive. Let’s begin with defining some variables. Enter the text in the screenshot into a new backup.sh script. Notice that we’ve misspelt ‘source’ as ‘sauce’, this is because there’s already a built-in command called ‘source’ hence the different spelling on our part.

### STEP 3

The previous script entries allowed you to create a Time Stamp, so you know when the backup was taken. You also created a ‘dest’ variable, which is the folder where the backup file will be created (/backups). You can now add a section of code to first check if the ~/backups folder exits, if not, then it creates one.

### STEP 4

Once the ~/backups folder is created, we can now create a new subfolder within it based on the Time Stamp variables you set up at the beginning. Add mkdir -p $dest/"$day $month $year". It’s in here that you put the backup file relevant to that day/month/year.

### STEP 5

With everything in place, you can now enter the actual backup routine, based on the Tar command from Step 5. Combined with the variables, you have: tar cvfz $dest/"$day $month $year"/DocumentsBackup.tgz $sauce. In the screenshot, we added a handy “Now backing up…” echo command.

### STEP 6

Finally, you can add a friendly message: echo “Backup complete. All done…”. The completed script isn’t too over-complex and it can be easily customised to include any folder within your Home area, as well as the entire Home area itself.

## Creating Bash Scripts
– Part 5

The backup script we looked at previously can be further amended to incorporate choices, user-interaction with regards to where the backup file will be copied to and so on. Automating tasks is one of the main benefits of Bash scripting, a simple script can help you out in many ways.

## EASY AUTOMATION AND HANDY SCRIPTS

Entering line after line of commands to retrieve system information, find a file or rename a batch of files? A script is a better answer.

### STEP 1
Let’s start by creating a script to help display the Mint system information; always a handy thing to have. Create a new script called sysinfo.sh and enter the following into Xed, or the text editor of your choice.

![](img/f80199d101da92d953f18eaa6205b48e_75_0.png)

### STEP 2
We’ve included a couple of extra commands in this script. The first is the -e extension for echo, this means it’ll enable echo interpretation of additional instances of a new line, as well as other special characters. The proceeding 31;43m element enables colour for foreground and background.

![](img/f80199d101da92d953f18eaa6205b48e_75_1.png)

### STEP 3
Each of the sections runs a different Terminal command, outputting the results under the appropriate heading. You can include a lot more, such as the current aliases being used in the system, the current time and date and so on. Plus, you could also pipe all that information into a handy HTML file, ready to be viewed in a browser.

![](img/f80199d101da92d953f18eaa6205b48e_75_2.png)

### STEP 4
Although there are simple Terminal commands to help you look for a particular file or folder, it’s often more fun to create a script to help you. Plus, you can use that script for other non-technical users. Create a new script called look4.sh, entering the content from the screenshot below.

![](img/f80199d101da92d953f18eaa6205b48e_75_3.png)

### STEP 5

When executed the script waits for input from the user, in this case the file extension, such as jpg, mp4 and so on. It’s not very friendly though. Let’s make it a little friendlier. Add an echo, with echo -n "Please enter the extension of the file you’re looking for: ", just before the read command.

```
#!/bin/bash
target=~
read name
output=$( find "$target" -iname "*$name*" 2> /dev/null )
if [[ "$output" ]]; then
  echo "$output"
else
  echo "No match found"
fi
```

### STEP 6

Here’s an interesting, fun kind of script using the app espeak. Install espeak with sudo apt-get install espeak, then enter the text below into a new script called speak.sh. As you can see it’s a rehash of the first greeting script we ran. Only this time, it uses the variables in the espeak output.

```
#!/bin/bash
echo "Hello, what is your first name?"
read firstname
echo "Hello $firstname, and what is your surname?"
read surname
espeak "Hello $firstname $surname, how are you on this fine $(date +%A)?"
```

### STEP 7

We briefly looked at putting some colours in the output for our scripts. Whilst it’s too long to dig a little deeper into the colour options, here’s a script that outputs what’s available. Create a new script called colours.sh and enter the text (see below) into it.

```
#!/bin/bash
clear
echo "\e[0m Normal\t\e[1m Bold\t\e[4m Underlined"
echo "\e[0m Normal\t\e[1m Bold\t\e[4m Underlined"
... [colour output script]
```

### STEP 8

The output from colours.sh can, of course, be mixed together, bringing different effects depending on what you want to the output to say. For example, white text in a red background flashing (or blinking). Sadly the blinking effect doesn’t work on all Terminals, so you may need to change to a different Terminal.

![](img/f80199d101da92d953f18eaa6205b48e_76_0.png)

### STEP 9

Whilst we’re on making fancy scripts, how about using Zenity to output a graphical interface? Enter what you see below into a new script, menu.sh. Make it executable and then run it. You should have a couple of dialogue boxes appear, followed by a final message.

```
#!/bin/bash
firstname=$(zenity --entry --title "Your Name" --text "What is your first name?")
surname=$(zenity --entry --title "Your Name" --text "What is your surname?")
zenity --info --title "Greetings" --text "Hello $firstname $surname, ..."
```

### STEP 10

While gaming in a Bash script isn’t something that’s often touched upon, it is entirely possible, albeit, a little basic. If you fancy playing a game, enter wget http://bruxy.regnet.cz/linux/housenka/housenka.sh, make the script executable and run it. It’s in Polish, written by Martin Bruchanov but we’re sure you can modify it. Hint: the title screen is in Base64.

![](img/f80199d101da92d953f18eaa6205b48e_76_1.png)
