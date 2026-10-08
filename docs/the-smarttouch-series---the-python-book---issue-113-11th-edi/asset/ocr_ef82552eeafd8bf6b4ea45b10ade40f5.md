# # Python essentials

```
```
14  iterations = 0
    while iterations < rerolls:
        iterations = iterations + 1
        replacement = dice_rerolls[iterations-1]
        dice[dice_changes[iterations-1]] = replacement

15  dice.sort()
    for i in range(len(dice)):
        print "Dice,"i + 1:"",names[dice[i]]

    result = hand(dice)
    print "You finish with", result

16  def roll(roll_number):
    numbers = range(1,7)
    dice = range(roll_number)

17  iterations = 0
18  while iterations < roll_number:
        iterations = iterations + 1
        dice[iterations-1] = random.choice(numbers)

    return dice
```
```

![](bbox=[0.0, 0.48, 0.4, 0.55])

# ### 14 New dice

We’re resetting and reusing the iterations variable to perform a similar while loop to update the rolls we’ve done to the original dice variable. The main part of this loop is using the iterations-1 variable to find the number from dice_changes list, and using that to change that specific integer in the dice list with the number from the replacement list. So if the first item on the dice_changes list is 2, then the second item on the dice list is changed to the number we want to replace it with.

# ### 15 Sorting

We’re ending the throw function in basically the same way we ended the first throw. First of all, we re-sort the dice list so that all the numbers are in ascending order. Then we print out the final cards that the dice correspond to, before again passing it onto the hand function so that we can fully determine the hand that the player has. We print out this result and that ends the function, sending the whole thing back to the game function so if you want to play again.

# ### 16 Dice rolling

The roll function is used twice in the code for both times that we roll the dice. Being able to use the same code multiple times means we can cut down on bloat in the rest of the script, allowing it to run a little faster, as we explained. It also means in this case that we can use it again if you want to change the game to three rounds, or modify it for real poker.

# ### 17 Number of rolls

We begin the whole thing by bringing over the roll_number variable into the function – this is because while in the original roll it will always be five, the second roll could between one and the full five. We create a list with the number of entries we need for each roll, and again set an iterations variable for the upcoming while loop.

# ### 18 Remember

Much like the while loops in the rest of the code so far, we’re keeping it going until iterations is the same as roll_number. Each entry in the dice list is replaced with a random number using the random.choice function and keeping it in the range of the numbers variable, which is one to six for each side of the dice. After this is done, we return the dice variable to the throw function that makes up the majority of a game.

# ### 19 Hand analysis

While not technically a hand of cards, the poker terminology still applies. We start in this function by setting up a few things. The first part uses the groupby function we imported – this is used in this case to count the numbers that make up the dice variable. If there are three twos, a four and a six, it will return [3, 1, 1], using this to ascertain what kind of hand the player has. As the output of this groupby won’t be in any specific order, we use the sort function again to sort it; however, this time we use the reverse=True argument to make the analysis easier again.

# ### 20 Straights

Straights and high cards are odd ones out in poker dice, as they are not rely on being able to count any repetitions in the cards. There are, however, only two hands that create a straight in poker dice, so we have created two lists here that contain them. We can then check first to see if the dice make these hands, and then if all other checks fail, it has to be a high card.

# ### 21 Your hand

While seemingly lengthy, this a fairly simple if statement. As we stated before, we check to see if it’s one of the two straight hands, as there are no flushes or royal straight flushes in poker dice, we don’t have to worry about those. We then check to see if the first item in the list is five, which can only result in five of a kind; similarly, if the first item is four then the hand must be four of a kind. If the first number is three, then it can be either a full house or three of a kind.

# HIGHER OR LOWER

Which hand is best? What are the odds of getting certain hands in the game? Some of the answers are surprising, as the poker hands they’re based on trump the differing odds the dice produce. We’ve ranked hands from highest to lowest.

+   - Five of a Kind ........................... 6/7776
- Four of a Kind ........................... 150/7776
- Full House ........................... 300/7776
- Straight ........................... 240/7776
- Three of a Kind .................... 1200/7776
- Two Pairs ........................... 1800/7776
- One Pair ........................... 3600/7776
- High Card ........................... 480/7776