
## Create with Python

```
def build(self):
    return TicTacToeGrid()
    # Replaces the previous label
```

With this complete you can run your main Python file again and enjoy your new program. All being well, the single Label is replaced by a grid of nine buttons, each of which you can click; it will automatically change colour and release (you’ll see the printed output information from our binding). We could customise the appearance by modifying other properties of the Button, but for now we’ll leave them as they are.

## Has anyone won yet?

We’ll want to keep track of the state of the board to check if anyone has won, which we can do with a couple more Kivy properties:

```
from kivy.properties import \
    (ListProperty, NumericProperty)

class TicTacToeGrid(GridLayout):
    status = ListProperty([0, 0, 0,
                           0, 0, 0,
                           0, 0, 0])
    current_player = NumericProperty()
```

This adds an internal status list representing who has played where, and a number to represent the current player (1 for ‘O’, -1 for ‘X’). By placing these numbers in our status list, we’ll know if somebody wins because the sum of a row, column or diagonal will be +-3. Now we can update our graphical grid when a move is played (Fig. 02).

You can run your app again to see exactly what this did, and you’ll find that clicking each button now places an ‘O’ or ‘X’ as well as a coloured background depending on whose turn it is to play. Not only that, but you can only play one move in each button thanks to our status array keeping track of existing moves.

This is enough to play the game but there’s one vital element missing... a big pop-up telling you when you’ve won! Before we can do that, we need to add some code to check if the game is over.

![](img/3b256f430f51c98f1315671f6e4eec19_109_0.png)

Kivy properties have another useful feature here, whenever they change they automatically call an ‘on_propertyname’ method if it exists and dispatch a corresponding event in Kivy’s event system. That makes it very easy to write code that will run when a property changes, both in Python and kv language. In our case we can use it to check the status list every time it is updated, doing something special if a player has filled a column, row or diagonal.

```
def on_status(self, instance, new_value):
    status = new_value
    # Sum each row, column and diagonal.
    # Could be shorter, but let’s be extra
    # clear what’s going on
    sums = [sum(status[0::]),  # rows
            sum(status[1::]),
            sum(status[2::]),
            sum(status[::3]),  # columns
            sum(status[1::3]),
            sum(status[2::3]),
            sum(status[::4]),  # diagonals
            sum(status[2::4])]
    # Sums can only be +-3 if one player
    # filled the whole line
    if 3 in sums:
        print("O’s win!")
    elif -3 in sums:
        print("X’s win!")
    elif 0 not in self.status:  # Grid full
        print("Draw!")
```

This covers the basic detection of a won or drawn board, but it only prints the result to stdout. At this stage we probably want to reset the board so that the players can try again, along with displaying a graphical indicator of the result (Fig. 03).

Finally, we can modify the ‘on_status’ method to both reset the board and display the winner in a ModalView widget.

```
from kivy.uix.modalview import ModalView

This is a pop-up widget that draws itself on top of everything else rather than as part of the normal widget tree. It also automatically closes when the user clicks or taps outside it.

winner = None
if -3 in sums:
    winner = 'X’s win!'
elif 3 in sums:
    winner = 'O’s win!'
elif 0 not in self.status:
    winner = 'Draw...nobody wins!'

if winner:
    popup = ModalView(size_hint=(0.75, 0.5))
    victory_label = Label(text=winner,
```

```
font_size=50)
popup.add_widget(victory_label)
popup.bind(on_dismiss=self.reset)
popup.open()
```

This mostly uses the same ideas we already covered, adding the 'Label' widget to the 'ModalView' then letting the 'ModalView' take care of drawing itself and its children on top of everything else. We also use another binding: this time to 'on_dismiss', which is an event dispatched by the 'ModalView' when it is closed. Finally, we made use of the 'size_hint' property common to all widgets, which in this case is used to set the 'ModalView' size proportional to the window - while a 'ModalView' is open you can resize the window to see it dynamically resize, always maintaining these proportions. This is another trick made possible by a binding with the 'size_hint' Kivy property, this time managed internally by Kivy.
That's it, a finished program! We can now not only play tic-tac-toe, but our program automatically tells us when somebody has won, and resets the board so we can play again. Simply run your program and enjoy hours of fun!

## Time to experiment

This has been a quick tour through some of Kivy's features, but hopefully it demonstrates how to think about building a Kivy application. Our programs are built from individual Kivy widgets, interacting by having Python code run when their properties change (eg our 'on_status' method) or when they dispatch events (eg 'Button' 'on_release'). We also briefly saw kv language and experienced how it can automatically create bindings between properties.
You can find a copy of the full program on FileSilo, which you can reference to check you've followed everything correctly. We've also added an extra widget, the 'Interface', with a structure coded entirely in kv language that demonstrates how to add child widgets this way. You can test it by uncommenting the 'return Interface()' line in 'TicTacToeGrid.build()'. It doesn't do anything fundamentally different to what we already covered, but it does make extensive use of kv language's binding ability to automatically update a label showing the current player, and to resize the TicTacToeGrid so that it is always square to fit within its parent. You can play with all these settings to see exactly how it fits together, or try things like swapping out the different widget types to see how other widgets behave.

> Try swapping out the different widget types to see how other widgets behave

```
class TicTacToeGrid(GridLayout):
    def __init__(self, *args, **kwargs):
        super(TicTacToeGrid, self).__init__(*args, **kwargs)
        for row in range():
            for column in range():
                grid_entry = GridEntry()
                    coords=(row, column))
                grid_entry.bind(on_release=self.button_pressed)
                self.add_widget(grid_entry)

def button_pressed(self, instance):
    # Print output just to see what's going on
    print('{} button clicked!'.format(instance.coords))
```

```
def button_pressed(self, button):
    # Create player symbol and colour lookups
    player = {'0': 'O', '1': 'X'}
    colours = {'0': (1, 0, 0, 1), '1': (0, 1, 0, 1)}  # (r, g, b, a)
    row, column = button.coords  # The pressed button is automatically # passed as an argument

    # Convert 2D grid coordinates to 1D status index
    status_index = 3*row + column
    already_played = self.status[status_index]

    # If nobody has played here yet, make a new move
    if not already_played:
        self.status[status_index] = self.current_player
        button.text = {'0': 'O', '1': 'X'}[self.current_player]
        button.background_color = colours[self.current_player]
        self.current_player *= -1  # Switch current player
```

```
# Note the *args parameter! It's important later when we make a binding # to reset, which automatically passes an argument that we don't care about
def reset(self, *args):
    self.status = [0 for _ in range(9)]

    # self.children is a list containing all child widgets
    for child in self.children:
        child.text = ''
        child.background_color = (1, 1, 1, 1)

    self.current_player = 1
```

![](img/3b256f430f51c98f1315671f6e4eec19_110_0.png)
