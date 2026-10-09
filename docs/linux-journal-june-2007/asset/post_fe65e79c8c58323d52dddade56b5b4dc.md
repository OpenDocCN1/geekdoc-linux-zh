
strong value that can offer the GNU/Linux community allowing not every application, but a lot of applications that are not too tightly coupled, to the system internals to be written using a platform-independent programming mechanism. And, that's the chief value that Perl and Python and others were bringing to the platform. And we thought, well, it's a great fit.

Another driver in choosing the GPL was we felt that the behaviour that would lead to monopolistic abuse of the Java platform would typically be done in secret until it was launched. By using the GPL, people will find it very tricky to do extensive development in secret. So we felt that the GPL provided us with the strongest protection against mis-behaviour by monopolists in the Java platform.

If you want to join the board, you have to pay out a very large sum of money, you have to commit a certain number of engineers to work only on that, at the direction of the Eclipse community, and you have to guarantee to produce products that use the Eclipse core code within a year. And, for us to fulfill those requirements, we would need to drop NetBeans. And, NetBeans is a big part of our tools development.

## GM: Finally, what's your vision of the world where open source is a major part of computing?

**SP:** I actually think that we're in the middle of a pivot point in the way society functions. I believe the World Wide Web as the vehicle for popularising the Internet is producing something that is as impactful as the Industrial Revolution. And, I think during the next decade, we will see that process of changing how absolutely everything works rolling out in front of us. Pre-World Wide Web, most things that happened in the world were done on a hub-and-spoke basis where you'd have, for example, government in the middle and citizens on the end of the spokes. Or, you'd have industry in the middle and customers on the end of the spokes. I think the introduction of the World Wide Web has changed the basic topology of society from hub-and-spoke to mesh.

Because the software industry is so closely connected to the World Wide Web, it's been one of the first to be impacted. So I see open source as an inevitable consequence of the switch to a meshed world. It's, in my view, the dominant way that software is developed in a participation age. The way you make money is not by locking people in a license at the beginning, but rather by providing the capabilities people want once they're running things. In the meshed world, what helps you be successful in a business is influence. And, you get influence not by power but by being valuable. My vision is that we're switching over to this new world of influence instead of control, of value instead of power, of participation instead of distribution.

So, we can expect to see a rolling tide of change where the principles of the meshed society begin to be worked out in other areas, like politics, like journalism, like the way families function, like the way money is handled, represented and stored. All of these things will gradually fall under the influence of the meshed society. And, I think being at the forefront of working with that meshed society is going to serve Sun and the people in the Open Source communities very well!

## GM: In a speech a couple of years back, Sun's CEO Jonathan Schwartz argued that the GPL is “IP colonialism”, because he claimed it imposed on poorer countries “a rather predatory obligation to [give back] all their IP to the wealthiest nation in the world”. Why did he change his mind?

**SP:** Well, you know, this is an interesting thing to contemplate, because I'm not sure he was wrong. The GPL does require you to set aside commercial protections for your software. And, it is possible that the use of the GPL for the indigenous software industry, for example, in Brazil, might harm the Brazilian economy. If you actually read the argument that Jonathan was making at the time, it's a good academic argument. What made it controversial was that it was the Chief Operating Officer of Sun saying it.

## GM: To what extent is Sun now committed to opening up everything that it can?

**SP:** We're completely committed to open-sourcing every thing that we're able to. Jonathan Schwartz asserted that as our position about two years ago. We're well on the road to fulfilling that commitment.

## GM: Given this commitment to free software, and the Open Source community, wouldn't it be more sensible for Sun to join Eclipse rather than pushing NetBeans on its own?

**SP:** The deal here is once again how you view open source. Open source isn't something you join; it's something you do. And, Sun doesn't want to join the Eclipse community, just like IBM doesn't want to join the OpenOffice.org community. Why would we want to join a community that isn't making any code we want to use in a product?

[Eclipse] has significant disadvantages for Sun in the way that IBM decided to set it up. If

# Boots Linux in 1.69 seconds!

## TS-7300 High Security Linux FPGA Computer

![](img/526fd434dcfcf1b461b94c24ea170f36_50_0.png)

$219 (qty 1) \$189 (qty 100) 200 MHz CPU

-   ▪ Fanless, no heat sink, < 2 Watts
-   ▪ User-programmable After 208 Cyclone II FPGA
-   ▪ PCI/104 expansion bus
-   ▪ 10 COM ports, 55 DIO
-   ▪ 2 USB ports, 2 SD Card sockets
-   ▪ 2 10/100 Eternets
-   ▪ Matrix keypad & LCD ports VGA video 800x600
-   ▪ 1.69 s Linux-based bootloader
-   ▪ Runs Debian, supports Real-Time

One piece metal enclosure setup provides 4 high-current GPIO, 4 ADC, 2 DAC, 1 CAN for **$160**

Design your solution with one of our engineers

-   ▪ Over 20 years in business
-   ▪ Never discontinued a product
-   ▪ Engineers on Tech Support
-   ▪ Open Source Vision
-   ▪ Custom configurations and designs w/ excellent pricing and turn-around time
-   ▪ Most products stocked and available for next day shipping

See our website for options, peripherals and x86 SBCs

![](img/526fd434dcfcf1b461b94c24ea170f36_50_1.png)

We use our stuff, visit our TS-7200 powered website at www.embeddedARM.com (480) 837-5200

# Programming Python, Part I

![](img/526fd434dcfcf1b461b94c24ea170f36_51_0.png)

This tutorial jumps right in to the power of Python without dragging you through basic programming.

Python is a programming language that is highly regarded for its simplicity and ease of use. It often is recommended to programming newcomers as a good starting point. Python also is a program that interprets programs written in Python. There are other implementations of Python, such as Jython (in Java), CLPython (Common Lisp), IronPython (.NET) and possibly more. Here, we use only Python.

JOSÉ P. E. "PUPENO" FERNÁNDEZ

## Installing Python

Installing Python and getting it running is the first step. These days, it should be very easy. If you are running Gentoo GNU/Linux, you already have Python 2.4 installed. The packaging system for Gentoo, Portage, is written in Python. If you don't have it, your installation is broken.

If you are running Debian GNU/Linux, Ubuntu, Kubuntu or MEPS, simply run the following (or log in as root and leave out sudo):

```
sudo apt-get install python
```

One catch is that Debian's stable Python is 2.3, while for the rest of the distributions, you are likely to find 2.4. They are not very different, and most code will run on both versions. The main differences I have encountered are in the API of some library classes, new features added to 2.4 and some internals, which shouldn't concern us here.

If you are running some other distribution, it is very likely that Python is prepackaged for it. Use the usual resources and tools you use for other packages to find the Python package.

If all that fails, you need to do a manual installation. It is not difficult, but be aware that it is easy to break your system unless you follow this simple guideline: install Python into a well-isolated place, I like /opt/python/2.4.3, or whatever version it is.

To perform the installation, download Python, unpack it, and run the following commands:

```
...
./configure --prefix=/opt/python/2.4/
make
make install
```

This task is well documented on Python's README, which is included in the downloaded tarball; take a look at it for further details. The only missing task here is adding Python to your path. Alternatively, you can run it directly by calling it with its path, which I recommend for initial exploration.

## First Steps

Now that we have Python running, let's jump right in to programming and examine the language as we go along. To start, let's build a blog engine. By engine, I mean that it won't have any kind of interface, such as a Web interface, but it's a good exercise anyway.

Python comes with an REPL—a nice invention courtesy of the Lisp community. REPL stands for Read Eval Print Loop, and it means there's a program that can read expressions and statements, evaluate them, print the result and wait for more. Let's run the REPL (adjust your path according to where you installed Python in the previous section):

```
$ python
Python 2.4.3 (#1, Sep 1 2006, 18:35:05)
[GCC 4.1.1 (Gentoo 4.1.1)] on linux2
Type "help", "copyright", "credits" or "license" for
more information.
>>>
```

Those three greater-than signs (>>>) are the Python prompt where you write statements and expressions. To quit Python, press Ctrl-D. Let's type some simple expressions:

```
>>> 5
5
```

The value of 5 is, well, 5.

```
>>> 10 + 4
14
```

That's more interesting, isn't it?

There are other kinds of expressions, such as a string:

```
>>> 'Hello'
'Hello'
```

Quotes are used to create strings. Single or double quotes are treated essentially the same. In fact, you can see that I used double quotes, and Python showed the strings in single quotes.

Another kind of expression is a list:

```
>>> [1, 3, 2]
[1, 3, 2]
```

Square brackets are used to create lists in which items are separated by commas. And, as we can add numbers, we can add—actually concatenate—lists:

```
>>> [1, 3, 2] + [11, 3, 2]
[1, 3, 2, 11, 3, 2]
```

By now, you might be getting bored. Let's switch to something more exciting—a blog. A blog is a sequence of posts, and a Python list is a good way to represent a blog, with posts as strings. In the REPL, we can build a simple blog like this:

```
>>> ["My first post", "Python is cool"]
['My first post', 'Python is cool']
>>>
```

That's a list of strings. You can make lists of whatever you want, including a list of lists. So far, all our expressions are evaluated, shown and lost. We have no way to recall our blog to add more items or to show them in a browser. Assignment commands to the rescue:

```
>>> blog = ["My first post", "Python is cool"]
>>>
```

Now blog, a so-called variable, contains the list. Unlike in the previous example, nothing was printed this time, because it is an assignment. Assignments are statements, and statements don't have a return value. Simply evaluating the variable shows us the content:

```
>>> blog
['My first post', 'Python is cool']
```

Accessing our blog is easy. We simply identify each post by number:

```
>>> blog[0]
'My first post'
>>> blog[1]
'Python is cool'
```

Be aware that Python starts counting at 0.
