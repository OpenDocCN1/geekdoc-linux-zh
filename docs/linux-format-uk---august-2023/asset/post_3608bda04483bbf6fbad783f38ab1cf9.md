
![](img/5cfcf2f4448dccdd1c5c2a2851544557_90_0.png)

## Can you help inspire the next generation of coders?

![](img/5cfcf2f4448dccdd1c5c2a2851544557_90_1.png)

**Code Club** is a nationwide network of volunteer-led after-school clubs for children aged 9-11.

We're always looking for people with coding skills to volunteer to run a club at their local primary school, library, or community center for an hour a week.

You can team up with colleagues; a teacher will be there to support you, and we provide all the materials you'll need to help get children excited about digital making.

There are loads of ways to get involved!

So to find out more, join us at **www.codeclub.org.uk**

## CODING ACADEMY

**MU**

Credit: https://codewith.mu

Part One! Don’t miss next issue, subscribe on page 16!

### Code your own Python text adventure

Nate Drake guides you through creating your own interactive text adventure with the power of Python, starting with the basics...

![](img/5cfcf2f4448dccdd1c5c2a2851544557_91_0.png)

- **OUR EXPERT**
- Nate Drake wants to dedicate this series to his dad, who once told him that no one was ever going to pay him to sit around and play video games.

Those of us old enough to remember the ‘70s and early ‘80s know that games were graphically very uninspiring, not to mention the fact that personal computers were still prohibitively expensive. In 1975, MIT student William Crowther took some time out of his busy schedule developing ARPANET to create a text adventure game he could play with his kids. Although it wasn’t the first of its kind (that honour belongs to 1973’s *Hunt the Wumpus*), Colossal Cave Adventure quickly spread over the early internet after heavy modifications. The basic premise was the same as any text adventure, in that you entered commands, such as the cardinal points of the compass (N, S, E and W), to move between areas, and interact with items, traps and monsters in a bid to win through to the end with maximum points.

Younger readers may find it difficult to believe that people actually still do this for fun. In fact, IF (interactive fiction) has never been more popular. The annual XYZZY Awards even offer prizes to those who code the very best text adventure games. In this four-part series, we plan to take you through the basic steps of creating your own text adventure game using the Python 3 programming language. The good news is that since it’s text-based, you won’t need a degree in Photoshop wizardry. It’s also a great programming project for getting started with Python, as well as developing clean coding practices. If you’re a Linux user, there’s more good news, because support for Python 3 is almost certainly already built into your distro. You can just type *python3* via the terminal to get started. Still, this isn’t the easiest way to code and run Python scripts, so we’ve used the Mu Python interpreter instead. It’s available in the Ubuntu software centre and it offers a quick and easy way to run scripts. Mu’s also available for the Raspberry Pi.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_91_1.png)

- **QUICK TIP**
- To download all the code samples for part one of this series, open a terminal and install Git via *sudo apt-get install git*. Next run *git clone https://github.com/aagreate/bpython-textadventure.git*. The files download to the 'bpython adventure' folder in your home directory.

Starting with how **not** to do it... In the first part of this guide, we’re going to focus on getting set up and world-building. In other words, you will learn how to create rooms in your underground cavern, dungeon or mystical world, as well as navigate between them.

It’s very easy to imagine that this is a lot easier than it is. For instance, try pasting this script into your Python interpreter and running it:

```python
print("Which way will you go?")
action_input = input('Action: ')
if action_input == 'n':
    print('To the North, you see the skeleton of a dwarf holding an axe.')
elif action_input == 's':
    print('To the South, you see an antique wooden chest. It’s locked.')
elif action_input == 'e':
    print('You see entrance to the cave where you arrived earlier. The gate is locked.')
elif action_input == 'w':
    print("To the west you see an iron grille set into the wall.")
else:
    print("You cannot go that way.")
```

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_0.png)

If you're using **Mu**, remember that you need to save code with a valid filename, such as `test1.py`, before you can run the script.

In order to break this code down, the `print` command is being put to fine use here. Setting the variable `action_input`, then matches any of the lower-case letters `n, s, e` or `w` so that the script prints out a description of the new room.

The `elif` command is Python's shortened version of `ELSE IF`, which simply means if the input doesn't match, to carry out another query. If you don't input a valid direction, this script just tells you, "You cannot go that way."

While you can code an adventure in this way, it will cause headaches later on. Firstly, you are probably going to want to have more than five rooms. This means you'll have to include more lines of `print` and `elif` commands to describe each one. Most text adventures also allow you to interact with the room in some way. What if you want to pick up the axe or try to open the gate?

Since you're probably going to want to do other things besides drift between rooms in future, it's best to define movement as a specific function. You can create functions using the `def` command in Python. The syntax is quite simple, for example:

```python
def hello_world():
    print("Hello World")
```

You can then call this function by just inserting `hello_world()` anywhere into your script.

As things stand, this script simply exits gracefully as soon as you've moved to one room. Luckily, Python lets you use the `while` command to loop code, which you can insert into your new `move` function:

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_1.png)

```python
def move():
    print("Which way will you go?")
    while True:
        action_input = get_player_command()
        if action_input in ['n', 'N']:
            print("To the North, you see the skeleton of a dwarf holding an axe.")
        elif action_input in ['s', 'S']:
            print("To the South, you see an antique wooden chest. It's locked.")
        elif action_input in ['e', 'E']:
            print("To the East, you see entrance to the cave.")
        elif action_input in ['w', 'W']:
            print("To the west you see an iron grille set into the wall.")
        else:
            print("You cannot go that way.")

def get_player_command():
    return input('Action: ')

move()
```

This version of the code is a slight improvement. There's now a defined function for moving. Players can

> **Mu** is an excellent Python editor. You can write and run code from within the program. Make sure to save first.

### MAPPING YOUR WORLD

Back in the day, budding game designers would create the maps for their text adventures using graph paper and a lot of patience. You're welcome to try this if it tickles your fancy, but there are more modern alternatives.

One of these is **IFMapper** (https://tinyurl.com/ifmapper). This handy tool enables you to plot individual rooms, map routes between them and even list a room description and items.

Doing this now will give you a much clearer idea of how to code the game later on. IFMapper's written in Ruby, so to get started, run `sudo apt-get install ruby` in the terminal.

Install the dependencies by running `sudo apt-get install build-essential libfox-1.6-dev ruby-dev libxrandr-dev` then install IFMapper itself with `sudo gem install ifmapper`. You can now run the program at any time by typing IFMapper into the terminal.

Once the program launches, go to `File > Save` and give your map a memorable name.

Click on any box in the grid to create a new Location. Double-click it to change the name, such as Main Cavern. You can use the other tabs to add a list of items in the room (if there are any), as well as a description. Click the dotted lines between rooms to represent a route between them. You can delete a route or room simply by clicking on it and then pressing Del.

If you need some inspiration, go to `File > Open` and check out the maps directory for some examples.

![](img/5cfcf2f4448dccdd1c5c2a2851544557_92_2.png)

Tools such as IFMapper enable you to easily plot out the areas and rooms in your game.
