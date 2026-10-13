Notice how a single echo command is used to display the full multi-line menu, taking advantage of the fact that the quotes preserve formatting and embedded newlines. Then `read` gets the selection from the user and stores it in the variable `choice`.

A case statement determines what choice was made. If choice 1 was selected, the user wants to look up someone in the phone book. In that case, the user is asked to enter the desired name, and the `lu` program is called with the specified argument. Note also that the double quotes around `name` in

```
lu "$name"
```

are necessary to ensure that two or more words typed in by the user are handed to `lu` as a single argument.

A similar sequence occurs if the user selects menu items 2 or 3.

The programs `lu`, `rem`, and `add` are from earlier chapters.

Here are some sample runs of `rolo`:

```
```text
$ rolo

Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book

Please select one of the above (1-3): 2
Enter name to be added: El Coyote
Enter number: 212-567-3232
$ rolo
```
```

*Try it again*

```
```text
Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book

Please select one of the above (1-3): 1

Enter name to look up: Coyote
El Coyote        212-567-3232
$ rolo
```
```

*Once again*

```
```text
Would you like to:

    1.  Look someone up
    2.  Add someone to the phone book
    3.  Remove someone from the phone book
```
```