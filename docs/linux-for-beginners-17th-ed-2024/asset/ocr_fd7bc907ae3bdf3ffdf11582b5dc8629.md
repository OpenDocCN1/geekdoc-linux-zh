# # Creating Bash Scripts – Part 3

In the previous pages we looked at some very basic Bash scripting, which involved outputting text to the screen, getting a user’s input, storing it and outputting that to the screen; as well as including a system variable using the Date command. Now let’s combine what you’ve achieved so far and introduce Loops.

# ## IF, THEN, ELSE

With most programming structures there will come a time where you need to loop through the commands you’ve entered to create better functionality, and ultimately a better program.

+   **STEP 1** Let’s look at the If, Then and Else statements now, which when executed correctly, compare a set of instructions and simply work out that: If something is present, THEN do something, ELSE do something different: Create a new script called greeting2.sh and enter the text in the screenshot below into it.

+   **STEP 3** The next line, ELSE, is what happens if the variable doesn’t equal ‘David’. In this case it simply outputs to the screen the now familiar ‘Hello...’. The last line, the FI statement, is the command that will end the loop. If you have an if command without a FI command, then you get an error.

+   **STEP 2** Greeting2.sh is a copy of greeting.sh but with a slight difference. Here we’ve added a loop starting at the If statement. This means, if the variable entered is equal to David the next line, THEN, is the reaction to what happens, in this case it will output to the screen ‘Awesome name’, followed by the variable (which is David).

+   **STEP 4** You can obviously play around with the script a little, changing the name variable that triggers a response; or maybe even issuing a response where the first name and surname variables match a specific variable.

```
```
#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ]
then
  echo $firstname
```
```greeting.sh X
#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ]
then
  echo $firstname
```
```

```
```
$ mkdir scripts
$ cd scripts
$ nano greeting2.sh

#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ]
then
  echo $firstname
else
  echo Hello $surname
fi
```
```

```
```
david@david-mint ~ 
$ ./scripts
david@david-mint ~ 
$ ./scripts
Hello, what is your name? David
Thank you, and what is your surname? Hayard
Awesome name, $firstname $surname
```
```

```
```
#!/bin/bash

echo -n 'Hello, what is your name? '
read firstname
echo -n 'Thank you, and what is your surname? '
read surname
clear
if [ $firstname == 'David' ] && [ $surname == 'Hayard' ]
then
  echo $firstname $surname
else
  echo Hello $firstname $surname, how are you on this fine Wednesday?
fi
```
```