# **More about Variables**

Lists are another data type beneficial to talk about. A list is an array of values that are grouped together into a single variable. The single variable can then be used to call upon any of the “sub variables” it contains. They are mostly used for organization and grouping purposes, and also to keep related variables in a similar place. List variables are created by initializing them.

```
state = "Texas"
```

```
jack_info = [8, "West Elementary", state, "A"]
```

```
print ("Jack goes to {} in {}.".format(jack_info[1], jack_info[2]))
```

```
print ("He has a {} in math, even though he's only {}.".format(jack_info[3], jack_info[0]))
```

The list "jack_info" contains four values because we specify four different entries between the square brackets. They are just