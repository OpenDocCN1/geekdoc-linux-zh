# STEP 5

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

# STEP 6

Here’s an interesting, fun kind of script using the app espeak. Install espeak with sudo apt-get install espeak, then enter the text below into a new script called speak.sh. As you can see it’s a rehash of the first greeting script we ran. Only this time, it uses the variables in the espeak output.

```
#!/bin/bash
echo "Hello, what is your first name?"
read firstname
echo "Hello $firstname, and what is your surname?"
read surname
espeak "Hello $firstname $surname, how are you on this fine $(date +%A)?"
```

# STEP 7

We briefly looked at putting some colours in the output for our scripts. Whilst it’s too long to dig a little deeper into the colour options, here’s a script that outputs what’s available. Create a new script called colours.sh and enter the text (see below) into it.

```
#!/bin/bash
clear
echo "\e[0m Normal\t\e[1m Bold\t\e[4m Underlined"
echo "\e[0m Normal\t\e[1m Bold\t\e[4m Underlined"
... [colour output script]
```

# STEP 8

The output from colours.sh can, of course, be mixed together, bringing different effects depending on what you want to the output to say. For example, white text in a red background flashing (or blinking). Sadly the blinking effect doesn’t work on all Terminals, so you may need to change to a different Terminal.

![](bbox=[0.52, 0.23, 0.95, 0.56])

# STEP 9

Whilst we’re on making fancy scripts, how about using Zenity to output a graphical interface? Enter what you see below into a new script, menu.sh. Make it executable and then run it. You should have a couple of dialogue boxes appear, followed by a final message.

```
#!/bin/bash
firstname=$(zenity --entry --title "Your Name" --text "What is your first name?")
surname=$(zenity --entry --title "Your Name" --text "What is your surname?")
zenity --info --title "Greetings" --text "Hello $firstname $surname, ..."
```

# STEP 10

While gaming in a Bash script isn’t something that’s often touched upon, it is entirely possible, albeit, a little basic. If you fancy playing a game, enter wget http://bruxy.regnet.cz/linux/housenka/housenka.sh, make the script executable and run it. It’s in Polish, written by Martin Bruchanov but we’re sure you can modify it. Hint: the title screen is in Base64.

![](bbox=[0.52, 0.83, 0.95, 0.92])