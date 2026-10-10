```
fruits .4
supplements .2
nachos/salsa .15

Dogs, Cats -

dog food .5
dog treats .55
cat food .7
catnip .75
```

Notice that there are four blank lines in *Feed*. Those blank lines will show up in each of the next three examples. They are not forgotten by the sort command.

+   Now, Juana sorts all the lines in *Feed* into dictionary (in other words, alphabetical) order:

```
$ sort Feed<Enter>
```

```
cat food .7
catnip .75
chop .2
dog food .5
Dogs, Cats -
dog treats .55
Filename: /home/gutieja/admin/Feed
fruits .4
hay (alfalfa, timothy, etc) .8
nachos/salsa .15
oats .3
Rozinante, Dapple -
supplements .1
vegetables (fresh) .65
vegetables (old, rotten) .6
```

+   Now, she sorts alphabetically by the *second* character in the first word of each line:

```
$ cat Feed | sort +0.1<Enter>
```