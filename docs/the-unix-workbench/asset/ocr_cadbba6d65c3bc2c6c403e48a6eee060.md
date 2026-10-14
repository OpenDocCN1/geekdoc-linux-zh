```
egrep "(iss){2}" states.txt
```

## Mississippi

We could combine more quantifiers and capturing groups to dream up even more complicated regular expressions. For example, the following regular expression describes three occurrences of an "i" followed by two of any character:

```
egrep "(i.{2}){3}" states.txt
```

## Mississippi

The complex regular expression above still only matches "Mississippi".

# Character Sets

For the next couple of examples we’re going to need some text data beyond the names of the states. Let’s just create a short text file from the console: