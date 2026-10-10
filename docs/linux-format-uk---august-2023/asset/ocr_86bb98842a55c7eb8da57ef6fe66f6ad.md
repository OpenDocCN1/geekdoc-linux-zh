# Text adventure CODING ACADEMY

```
```python
curly: [curly]
[0:0] [0:0] [0:0] [0:0]
23641902
[0:0] [0:0]
[0:0] [0:0] [0:0] [0:0] [0:0] [0:0] [0:0]
[0:0] [0:0]
[0:0] [0:0] [0:0]
[0:0] [0:0] [0:0] [0:0]
[0:0] [0:0] [0:0] [0:0]
[0:0] [0:0]
[0:0] [0:0] [0:0]
[0:0] [0:0]
[0:0] [0:0] [0:0] [0:0]
[0:0] [0:0]
[0:0] [0:0] [0:0]
[0:0] [0:0]
[0:0] [0:0] [0:0] [0:0]
[0:0] [0:0] [0:0] [0:0] [0:0] [0:0] [0:0]
```
```

Although this script doesn’t appear any different to players, under the hood it’s using the `room` class to load new areas.

```
```python
print("You cannot go that way.")

def get_player_command():
    return input('Action: ')

move()
```
```

- As you can see, the game begins by placing the player in room1 (Main Cavern). The newly tweaked move function displays the current room name and description before asking you where to go.

- Once you choose a direction, move changes the player’s location to another room, then reloads the move command to read out the name and description of that room. Try running the script and moving between rooms so you can see the code in action.

- You can download an example of this script from https://tinyurl.com/lkfpythonstmove2.

# Where’s the exit?

You may have noticed that even with our `room` and `player` objects nicely defined, you can still move from any room to any other. You can get around this by updating the `room` class to have clearly defined exits:

```
```python
class room:
    def __init__(self, name, description, exits):
        self.name = name
        self.description = description
        self.exits = exits
```
```

This means when you define your `room` object, you also need to list the exits for them. You can do this using a list of values. Set them to `None` for now: `room1 = room(1, “Main Cavern”, “You are standing in a dark cavern. You hear the sound of dripping water.”, [None, None, None, None])`

We do this because Python can’t recognise objects until you declare them in the script. Once you’ve listed all the rooms, you can then add the exit rooms. There are four different list values to represent the four points of the compass (N, S, E and W), for example: `room1.exits = [room2, room3, room4, room5]`

The `exits` attribute now shows that the player can go north, south, east and west into `room2`, `room3`, `room4` and `room5` respectively.

You can then update the `move` function to check for valid exits:

```
```python
def move():
    print(player.currentroom.name)
    print(player.currentroom.description)
```
```

```
```python
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
```

- The function has been modified so that when the player inputs a command, this must not only be a valid direction (N, S, E or W), but the corresponding `exits` value for the current room must be another room. If so, then the player is taken there.

- You can download an example of this script with exits set up for all five rooms from https://tinyurl.com/lkfpythontestmove3.

# Dropping off the map

By now, believe it or not, you’ve learned almost all the essential code to create your very own Python text adventure. The remaining parts of this series will make good use of the code you’ve seen so far to allow your player to interact with items, fight the bad guys and even add some simple graphics.

- If you run into any errors in your interpreter, make sure all your variables and commands are correctly spelled. Python also places great streak in indented code. If you’re still having difficulties, feel free to download and run a copy of all the code so far from https://tinyurl.com/lkfpythonstmove4.

![](bbox=[0.44, 0.63, 0.8, 0.92])

By adding the `text` attributes to the `room` class, you can specify which rooms can be accessed from others.

QUICK TIP For simplicity, we’ve placed all the code for the game in one simple script. A competent Python programmer would probably split a game into several files then call from the main script. Read more at https://docs.python.org/3/tutorial/modules.html

OUR SUBS SITE IS AN ADVENTURE! Subscribe now at http://bit.ly/LinuxFormat