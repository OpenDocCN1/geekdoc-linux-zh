```
until [ "$i" -gt $UPPER_LIMIT ]
do
Deck[i]=$UNPICKED    # Set each card of "Deck" as unpicked.
let i += 1
done
echo
{}
```

```
initialize_Suits ()
{
Suits[0]=C #Clubs
Suits[1]=D #Diamonds
Suits[2]=H #Hearts
Suits[3]=$Spades
}
```

```
initialize_Cards ()
{
Cards=(2 3 4 5 6 7 8 9 10 J Q K A)
# Alternate method of initializing an array.
```

```
pick_a_card ()
{
card_number=$RANDOM
let card_number %=$CARDS # Restrict range to 0 - 51, i.e., 52 cards.
if [ "${Deck[card_number]}" -eq $UNPICKED ]\nthen
Deck[card_number]=$PICKED
return $card_number
else
return $DUPE_CARD
fi}
```

```
parse_card ()
number=$1
let suit_number = number / CARDS_IN_SUIT
suit=${Suits[suit_number]}
echo -n "$suit"
let card_no = number % CARDS_IN_SUIT
Card=${Cards[card_no]}
printf "-%4s $Card"
# Print cards in columns.
```

```
seed_random ()
# Seed random number generator.
{
# What happens if you don't do this
let seed=$seed % 32766
RANDOM=$seed
# Consider other methods of seeding the random number generator.
```

```
deal_cards ()
{
cards_picked=0
while [ "${cards_picked}" -le $UPPER_LIMIT ]
do
pick_a_card
```

Chapter 37. Bash, versions 2, 3, and 4