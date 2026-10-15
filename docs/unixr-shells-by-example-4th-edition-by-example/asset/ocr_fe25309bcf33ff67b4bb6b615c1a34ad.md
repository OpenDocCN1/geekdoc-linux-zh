![](bbox=[0.157, 0.091, 0.608, 0.438])

**Figure 3.1** Remembered patterns and tags.

# EXAMPLE 3.11

```
```text
% vi textfile (Before substitution)

---------------------------------------------
Unusual occurrences happened at the fair.
Patty won fourth place in the 50 yard dash square and fair.
Occurrences like this are rare.
The winning ticket is 5222.
The ticket I got is 54333 and Dee got 55544.
Guy fell down while running around the south bend in his last event.
~
~
~
1  :s/\(square\) and \(fair\)/\2 and \1/
---------------------------------------------

% vi textfile (After substitution)
---------------------------------------------
Unusual occurrences happened at the fair.
--> Patty won fourth place in the 50 yard dash fair and square.
Occurrences like this are rare.
The winning ticket is 5222.
The ticket I got is 54333 and Dee got 55544.
Guy fell down while running around the south bend in his last event.
~
~
~
---------------------------------------------
```
```