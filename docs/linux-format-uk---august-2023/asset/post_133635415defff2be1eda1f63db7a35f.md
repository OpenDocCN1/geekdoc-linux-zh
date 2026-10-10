
## CODING ACADEMY: Text Adventure

### QUICK TIP

If you prefer not to install extra software, the terminal on most Linux distros can run Python perfectly well. To execute a script, just use the `python3` command plus the filename, such as `python3 adventure1.py`.

Now enter directions in upper or lower-case. After you've made a move, the game asks where to go next.

### A Touch of Class

Now that you have your movements down pat, it's time to start doing some world-building. This is where Python comes to the rescue through its use of classes and objects.

A class is best described as a kind of blueprint that allows you to define objects. A class defines the attributes a method can have. For instance, each room in your adventure will be in a specific location and have a specific description. To get started, define the `room` class by placing this code at the top of a new script:

```python
class room:
    def __init__(self, number, name, description, exits):
        self.number = number
        self.name = name
        self.description = description
```

Now that you've defined the `room` class, you can actually list a specific room below it, for example:

```python
room1 = room(1, "Main Cavern", "You are standing in a dark cavern. You hear the sound of dripping water.")
```

You can now interact with the object attributes from within your script using the format `object.attribute`. For instance, try adding these lines at the end of your code to see the `name` of the room and its `description`:

```python
print(room1.name)
print(room1.description)
```

This is fine for providing a description of the very first room, but what about when you move to others? Once again, classes and objects can come to the rescue. Return to the top of your script and create a `player` class below the `room` one, as follows:

```python
class player:
    def __init__(self, name, currentroom):
        self.name = name
        self.currentroom = currentroom
```

Now you can change the player's location – to `room1`, for example – and display the `name` and `description` for that room. Just add these lines to the bottom of your script and run it:

```python
player.currentroom = room1
print(player.currentroom.name)
print(player.currentroom.description)
```

Try adding other rooms besides `room1`. Next, try adding these lines to the end of your script:

```python
player.currentroom = room1

def move():
    print(player.currentroom.name)
    print(player.currentroom.description)
    print("Which way will you go?")
    while True:
        action_input = get_player_command()
        if action_input in ['n', 'N']:
            player.currentroom = room2
            move()
        elif action_input in ['s', 'S']:
            move()
        elif action_input in ['e', 'E']:
            player.currentroom = room4
            move()
        elif action_input in ['w', 'W']:
            player.currentroom = room5
            move()
        else:
            print("You cannot go that way.")

def get_player_command():
    return input('Action: ')

move()
```

### KEEPER OF THE KEYS

No text adventure would be complete without having the player negotiate locked doors. To get started, first create a `key` class at the top of your script:

```python
class key:
    def __init__(self, keyusedesc, keyroomdesc, keyexits):
        self.keyusedesc = keyusedesc
        self.keyroomdesc = keyroomdesc
        self.keyexits = keyexits
```

You should also update the `room` class to have an optional `key` attribute `self.key`. The `player` class also needs to be updated with their own `self.keyring` attribute, so the script can check if they have the `right key` for this `room`. So you can now create a specific `key` object below where the exits are defined:

```python
redkey = key("You use the red key to unlock the gate", "You see the entrance to the cave where you arrived earlier. The red gate lies open.", [None, None, room6, room1])
```

You can now add:

```python
room4.key = redkey
player.keyring = [None, None, None, None, redkey]
```

Finally, you need a function to check whether a key is required for the current `room` and to use it if so:

```python
def checkkeys():
    currentroom = player.currentroom
    if currentroom.key != None and currentroom.key in player.keyring:
        print(currentroom.key.keyusedesc)
        currentroom.description = currentroom.key.keyroomdesc
        currentroom.exits = currentroom.key.keyexits
        currentroom.key = None

checkkeys()
```

If the player has a key for a room, they'll see a message saying they've used the key. The room description and exits are also updated accordingly.
You can find a full example of this script at https://tinyurl.com/byxpthontestmove4/ .

![](img/5cfcf2f4448dccdd1c5c2a2851544557_93_0.png)

> Famous text adventure games, such as Zork, have locked doors, making you either find the right key or another way in.

Although this script doesn't appear any different to players, under the hood it's using the `room` class to load new areas.

- As you can see, the game begins by placing the player in room1 (Main Cavern). The newly tweaked `move` function displays the current room name and description before asking you where to go.
- Once you choose a direction, `move` changes the player's location to another room, then reloads the `move` command to read out the name and description of that room. Try running the script and moving between rooms so you can see the code in action.
- You can download an example of this script from https://tinyurl.com/lkfpythonstmove2 .

### Where's the Exit?

You may have noticed that even with our `room` and `player` objects nicely defined, you can still move from any room to any other. You can get around this by updating the `room` class to have clearly defined exits:

```python
class room:
    def __init__(self, name, description, exits):
        self.name = name
        self.description = description
        self.exits = exits
```

This means when you define your `room` object, you also need to list the exits for them. You can do this using a list of values. Set them to `None` for now:

```python
room1 = room(1, "Main Cavern", "You are standing in a dark cavern. You hear the sound of dripping water.", [None, None, None, None])
```

We do this because Python can't recognise objects until you declare them in the script. Once you've listed all the rooms, you can then add the exit rooms. There are four different list values to represent the four points of the compass (N, S, E and W), for example:

```python
room1.exits = [room2, room3, room4, room5]
```

The `exits` attribute now shows that the player can go north, south, east and west into `room2`, `room3`, `room4` and `room5` respectively.

You can then update the `move` function to check for valid exits:

```python
def move():
    print(player.currentroom.name)
    print(player.currentroom.description)
    print("Which way will you go?")
    while True:
        action_input = get_player_command()
        if action_input in ['n', 'N'] and player.currentroom.exits[0] != None:
            player.currentroom = player.currentroom.exits[0]
            move()
        elif action_input in ['s', 'S'] and player.currentroom.exits[1] != None:
            player.currentroom = player.currentroom.exits[1]
            move()
        elif action_input in ['e', 'E'] and player.currentroom.exits[2] != None:
            player.currentroom = player.currentroom.exits[2]
            move()
        elif action_input in ['w', 'W'] and player.currentroom.exits[3] != None:
            player.currentroom = player.currentroom.exits[3]
            move()
        else:
            print("You cannot go that way.")

def get_player_command():
    return input('Action: ')
```

- The function has been modified so that when the player inputs a command, this must not only be a valid direction (N, S, E or W), but the corresponding `exits` value for the current room must be another room. If so, then the player is taken there.
- You can download an example of this script with exits set up for all five rooms from https://tinyurl.com/lkfpythontestmove3 .

### Dropping Off the Map

By now, believe it or not, you've learned almost all the essential code to create your very own Python text adventure. The remaining parts of this series will make good use of the code you've seen so far to allow your player to interact with items, fight the bad guys and even add some simple graphics.

- If you run into any errors in your interpreter, make sure all your variables and commands are correctly spelled. Python also places great stock in indented code. If you're still having difficulties, feel free to download and run a copy of all the code so far from https://tinyurl.com/lkfpythonstmove4 .

![](img/5cfcf2f4448dccdd1c5c2a2851544557_94_0.png)

By adding the `exits` attributes to the `room` class, you can specify which rooms can be accessed from others.

### QUICK TIP

For simplicity, we've placed all the code for the game in one simple script. A competent Python programmer would probably split a game into several files then call from the main script. Read more at https://docs.python.org/3/tutorial/modules.html

Our subs site is an adventure! Subscribe now at http://bit.ly/LinuxFormat
