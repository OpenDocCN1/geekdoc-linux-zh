![](bbox=[0.08, 0.16, 0.3, 0.24])

![](bbox=[0.44, 0.16, 0.78, 0.24])

At the end of the last tutorial (issue 166), our script was able to ask the user for the subject of the emails to be sent. Let’s recapitulate by taking a look at a small example:

```
#!/bin/bash

echo "Enter title!"

read emailTitle
echo emailTitle
```

```
if [ $emailShorty == "a" ]; then
	echo "Alert, electronics head detected!"
	 emailIitle="Analogue electronics tutorial!"

elif [ $emailShorty == "g" ]; then
	 emailTitle="Review of gadget"

elif [ $emailShorty == "r" ]; then
	 emailTitle="Review of book"

else
	echo "Error"
	exit
fi
```

After the hashbang designating the file to be a Bash script, we can now invoke the read command in order to get data from the command line. It is then written out once again via the echo function.

Bash requires the presence of the if clause; elif and else clauses are optional, but handy to keep your shell script more compact.

Forcing users to enter long texts is a classic dealbreaker in mobile: when working with desktop apps, it still should be avoided in the interest of usability. One effective way to improve your program’s behaviour involves guiding the user to their result.

The actual syntax of the if clause is quite useful. Selectors come in curly brackets and are terminated with a semicolon; the then clause starts the command list to be executed if the matcher hits.

> “Scripts will be able to reject invalid input on the fly, keeping clumsy or technically uninitiated users safe”

```
#!/bin/bash

echo "Choose the material!"
echo "...Analogue electronics tutorial!"
echo "g...Review of gadget"
echo "r...Review of book!"

read -n 1 emailShorty
```

However, there is one small niggle lurking for unsuspecting users. Be aware that the | must have a trailing space, while the ] needs a leading one – if they are missing, errors similar to the ones shown in the figure will occur. Furthermore, spaces are also needed on the left-hand and the right-hand side of the == operator.

read can be provided with one or more parameters which modify the behaviour. Passing -n 1 informs the command that we are looking for just one character – the user does not need to press return. Be aware that this can lead to awkward-looking console output – adding an empty echo "" after the read fixes the problem.

# Short hand expressions

As the collection of input from a specific set is an extremely common operation, Bash provides a shorthand expression for it. Its use would simplify our program as in the following:

```
echo "Choose the material!"

select emailTitle in "a...Analogue electronics tutorial!" "g...Review of gadget" "r...Review of book";
do
	echo $emailTitle
	break
done
```

# If this, then that!

Running the code snippet above leaves you with a variable containing – ideally – a single character’s worth of input. Transforming this into a usable e-mail title requires the usage of a structure commonly known as a selection. It takes its name from its habit of changing program execution in relationship to a variable. The most primitive form is the if selection, which can be deployed like this:

```
... 

read -n 1 emailShorty
echo ""
```

You should be aware that the break command is mandatory; the script will loop endlessly if you forget to include it, which isn’t what you want at all. Breaking out of this is best accomplished via the Ctrl + C sequence, which will lead you to the results shown in the figure.