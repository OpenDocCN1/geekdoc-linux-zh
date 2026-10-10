# Table 8.3 Selected grep Options

| OPTION | DESCRIPTION |
| :--- | :--- |
| -v | Print the lines that do not match the specified pattern. |
| -c | Print only a count of the matching lines. |
| -l | Print only the names of the files with matching lines. |
| -n | Print matching lines and their line numbers in the respective files. |
| -i | Ignore the case of the letters when making comparisons. |
| -w | Perform a whole word search. |

# grep Options

Table 8.3 presents some of the more common grep options. All of these options are used in Example 8.7, where we present the poem titled “Fleas.”

# Example 8.13 Applying grep to “Fleas”

Sancho, inspired by Don Quixote’s poetic prowess (questionable though these examples might be), has written this poem and has saved it in his home directory. After you read it, you will probably wonder why:

```
$ cat fleas<Enter>
Fleas

You bite those bugs and give a yelp
You scratch anon, sometimes it helps
You chase your tail, you drag your butt
Oh, but you’re suffering, my dear old mutt

I rub your belly and your back
To stem that burning itch attack
I scratch your ears, and scratch your head,
But those cursed fleas fill me with dread!

They are entrenched, they won’t go ‘way
Do what you will, they’re here to stay
You long for the “powders”, you yearn for the “collars”
Perhaps a mud pit in which to waller?

But, you know what? You see, old friend?
To rout those fleas, reach your happy end?
```