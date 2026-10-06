# Advanced Bash–Scripting Guide

```
case "$variable" in
  "$condition1"
    command...
    ;;
  "$condition2"
    command...
    ;;
```

esac

![](bbox=[0.309, 0.273, 0.342, 0.29])

+   - Quoting the variables is not mandatory, since word splitting does not take place.
- Each test line ends with a right paren).
- Each condition block ends with a double semicolon ::;
- The entire case block terminates with esac (case spelled backwards).

# Example 10–23. Using case

```
#!/bin/bash

echo "Hit a key, then return."
read Keypress

case "$Keypress" in
  [a-z]) echo "Lowercase letter";
  [A-Z]) echo "Uppercase letter";
  [0-9]) echo "Digit";
  *) echo "Punctuation, whitespace, or other";
# Allows ranges of characters in [square brackets]
esac

# Exercise:

# As the script stands, it accepts a single keystroke, then terminates.
# Change the script so it accepts continuous input,
# reports on every keystroke, and terminates only when "X" is hit.
# Hint: enclose everything in a "while" loop.
exit 0
```

# Example 10–24. Creating menus using case

```
#!/bin/bash

# Crude address database

clear # The screen.

echo "Contact List*"
echo "      ------ ---"
echo "Choose one of the following persons:"
echo
```

# 10.4. Testing and Branching