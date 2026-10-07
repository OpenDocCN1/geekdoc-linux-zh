# 226 Lab 5.1: Parameters

Double-Check: If the output is something like “Name Your0,” it means you forgot to put braces around the reference to variable 10, and the shell interpreted it as a reference to variable I, followed by the character O. It's a lot easier not to type in the braces, but when they are needed, there is no way around it.

![](bbox=[0.155, 0.096, 0.247, 0.153])

Now run the script again, but with each of the letters of the alphabet as parameters. Explain these results.

Answer:Your interaction should look like the following:
[5015]: s512 a b c d e f g h i j k l m n o p q r s t \ u v w x y z
a b c d e f g h i j
[5016]:

Only the first 10 parameters are printed because that's as many as were referenced in the print command. The other letters were passed and available, but there are no references to them in this script.

Create a function named f512 with the same print statement in it as s512. Run it twice, once with your name and once with the letters of the alphabet as parameters.

Is there any difference between running the function and running the script?
Answer:Your interactions should look like the following:
[5016]: f512 Your Name
Your Name
[5018]: f512 a b c d e f g h i j k l m n o p q r s t \ u v w x y z
a b c d e f g h i j
[5017]:

There's no difference between running the script and the function, as far as positional parameters are concerned. One major difference between scripts and functions is that the shell processes functions more efficiently than scripts. The other major difference is that functions run in the same context as the shell, whereas scripts run as separate processes. That is, running a function is like dotting a script.