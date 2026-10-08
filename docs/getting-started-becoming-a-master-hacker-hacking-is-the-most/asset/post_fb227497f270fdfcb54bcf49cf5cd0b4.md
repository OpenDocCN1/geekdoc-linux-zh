
![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_531_0.png)

Classes can also have subclasses. Our car class has an Audi subclass, and an object of that subclass might be an Audi A8.

Each object would have properties (make, model, year, and color) and methods (start, lock, drive, and park).

In OOP languages such as Python, objects inherit the characteristics of their class; the Audi A8 would inherit the methods (start, lock, drive, and park) from its class “car.”

These OOP concepts are critical to understanding how Python works, as you will see as you progress through this chapter, and your Python skills develop.

## Getting Started

Now that we have some of the basics out of the way, let’s talk about some basic programming concepts, terminology, and Python syntax. After that, we will begin to write some simple scripts evolving to some more sophisticated hacking scripts before the end of this chapter.

Just like BASH scripts, we can create Python scripts with any text editor such as vim or Leafpad. As your scripts advance into greater complexity and sophistication, you will likely find using an integrated development environment, or IDE, useful. In this chapter, we will use one of the best Python IDEs, PyCharm. IDEs are like text editors, but with additional capabilities built-in, such as color-coding, debugging, and compiling capabilities.

Although most IDEs will work in multiple programming environments, PyCharm is designed **exclusively** to work with Python. This is an excellent IDE with a lot of enhancements that will make your coding faster and more efficient. The professional version of PyCharm can be purchased, but we will use the free community edition here. You don’t need to use an IDE to follow on in this chapter, but it will help.

You can download PyCharm from [https://jetbrains.com/pycharm/download](https://jetbrains.com/pycharm/download). Once it has downloaded, you will need to navigate to the new PyCharm directory, extract it, and then start PyCharm by executing the pycharm.sh script.

```
root@kali-2019:~/pycharm-community-2019.2.3# cd bin
root@kali-2019:~/pycharm-community-2019.2.3/bin# ls -l
total 196
-rwxr-xr-x 1 root root    221 Sep 25 02:50 format.sh
-rw-r--r-- 1 root root   26540 Sep 25 02:50 fsnotifier.sh
-rwxr-xr-x 1 root root   32776 Sep 25 02:50 fsnotifier64
-rw-r--r-- 1 root root   26453 Sep 25 02:50 fsnotifier-arm
-rw-r--r-- 1 root root    10915 Sep 25 02:50 idea.properties
-rwxr-xr-x 1 root root     296 Sep 25 02:50 inspect.sh
-rw-r--r-- 1 root root   39520 Sep 25 02:50 libdbm64.so
-rw-r--r-- 1 root root    2322 Sep 25 02:50 log.xml
-rwxr-xr-x 1 root root     410 Sep 25 02:50 m2-intern.py
-rw-r--r-- 1 root root     533 Sep 25 02:50 pycharm64.vmoptions
-rw-r--r-- 1 root root    7074 Sep 25 02:50 pycharm.png
-rwxr-xr-x 1 root root     739 Sep 25 02:50 pycharm.sh
-rw-r--r-- 1 root root    4774 Sep 25 02:50 pycharm.svg
-rw-r--r-- 1 root root     541 Sep 25 02:50 pycharm.vmOptions
-rwxr-xr-x 1 root root     808 Sep 25 02:50 restart.py
root@kali-2019:~/pycharm-community-2019.2.3/bin$ pycharm.sh
bash: pycharm.sh: command not found
root@kali-2019:~/pycharm-community-2019.2.3/bin$ . ./pycharm.sh
OpenJDK 64-Bit Server VM warning: Option UseConcMarkSweepGC was deprecated in version 9.0 and will likely be removed in a future release.
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_533_0.png)

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_533_1.png)

This should open the PyCharm interface that looks like the figure below.

## Variables

Let’s begin with some of the more practical concepts in Python. Like in other programming languages, Python has variables. A variable is a name associated with a particular value. Whenever you use that variable name in a program, it uses the associated value. For instance, a variable called “name” might contain the value “OccupyTheWeb.”

A variable name points to data stored in a memory location, which may contain a value such as an integer, real number, string, floating point number, Boolean value (TRUE or FALSE), list or dictionary (we'll cover these shortly).

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_534_0.png)

```python
#!/usr/bin/python3

name="OccupyTheWeb"

print ('Greetings to ' + name + ' and Welcome To This Journey To Become a Master Hacker!')
```

```bash
root@kali-2019:~#  ./first_simple_script.py
Greetings to OccupyTheWeb and Welcome To This Journey to Become a Master Hacker!
root@kali-2019:~# 
```

To become familiar with variables, let’s create our first Python script. Open your PyCharm IDE and create the following simple script you can call first_simple_script.py.

The first line simply tells the system to use the python3 interpreter (Python3 is the latest Python, but many systems still use Python2.7 at this writing). The second line defines a variable called name and assigns a value to it (in this case, “OccupyTheWeb”). You can change this line to your name or any name.

The value of this variable is in the string character data format, which means the content is enclosed in quotation marks and is treated as text (Note: in Python, single or double quotation marks are generally interchangeable with some exceptions). You can put numbers in strings, but they will be treated as text and not numbers.

The third line creates a print() statement concatenating (“concatenate” is a fancy word used in information technology, meaning “put together”) “**Greetings to**” with the value in the **name** variable followed by the text “**and Welcome to This Journey to Become a Master Hacker**.” A print statement will display whatever you pass to it within the parenthesis to the screen.

Before you can execute this script, you need to give yourself permission to execute it. You need to use the chmod command to do that.

`kali > chmod 755 first_simple_script.py`

Now, to execute the script, simply precede the script name with a period and forward slash (./).

`kali > ./first_simple_script.py`

Success! You just completed a very basic script in Python!

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_536_0.png)

```python
#!/usr/bin/python3

HackersAriseStringVariable = "Getting Started Becoming a Master Hacker";

HackersAriseIntegerVariable = 12

HackersAriseFloatingPointVariable = 3.1415

HackersAriseList = [1,2,3,4,5,6]

HackersAriseDictionary = {'name' : 'OccupyTheWeb', 'value' : 27}

print (HackersAriseStringVariable)

print (HackersAriseIntegerVariable)

print (HackersAriseFloatingPointVariable)

print (HackersAriseList[3])
```

In Python, each variable type is treated like a class. A class is a template for creating objects (as we discussed in the earlier section on OOP). In the next script, I will demonstrate a few different types of variables. Variables can be more than just strings (text). They can hold several different data types.

This script creates five variables that contain different data types. These include:
- A string - treated as text
- An integer — a number without decimals
- A floating-point number — a number with decimals
- A list — a series of values stored together
- A dictionary — an unordered set of data each with its own key

Dictionaries are useful when you want to refer to or change a value by referring to a key name. For example, say you have a dictionary called cars that contains your favorite model of each car manufacturer configured like the following: `cars = {'BMW' : 'X6', 'Mercedes' : 'GLC300', 'Tesla': 'Model X', 'Audi' : 'Q3'}`

Later, while writing your script, you may want to get your favorite model of a particular car, you can simply call it by its key.

```
print (cars['BMW'])
```

![](img/ae0bf680ecd2ea15f7b4172e1f4a3412_537_0.png)

You can also change the values for particular keys. If you wanted to change your favorite Tesla to the Model S, you would enter: `cars['Tesla'] = 'Model S'`

We will discuss lists and dictionaries in more detail later in this chapter.

Enter the script above in PyCharm and save it as secondscript.py. Give yourself permission to execute it and then execute it as follows: `kali > ./secondpythonscript.py`
