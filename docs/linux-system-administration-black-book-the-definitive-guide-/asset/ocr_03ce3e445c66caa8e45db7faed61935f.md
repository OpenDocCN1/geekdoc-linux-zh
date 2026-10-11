![](bbox=[0.0, 0.09, 0.06, 0.25])

# # Pattern Matching

A critical skill for many applications is your ability to set up regular expressions. These statements are used to establish a pattern. The tool you are using then compares this pattern against the data it was told to examine. Some programs sometimes use slightly different pattern-matching characters than other programs use, but in general, many tools share the same pattern-matching habits.

The first thing you must know to build a pattern is what you are looking for. After you narrow down the common characteristics of what you want to find, you can then reach into your metacharacter—a character that represents information about other characters—toolbox and, as closely as possible, represent what it is you are looking for. The trick is that you also want to make sure that the things you are not looking for do not show up.

# ## Characters

The most basic metacharacters available are those that refer to one or more individual characters. Two characters that are used for this function and that are available in almost all parsing tools are the period and the asterisk. You can use a period to specify that a single unknown item is missing from the pattern. For example, suppose you are looking for the permissions and ownerships on the series of files house1, house2, and house3. Typing the following in the directory containing those files would find it properly:

```
```
ls -la house.
```
```

The asterisk enables you to specify that one or more characters are unknown. Suppose that, along with the house files, you also had these files:

+   - car1, car2, and car3
+   - dog1, dog2, and dog3
+   - yard1, yard2, and yard3

For each set of 1’s, 2’s, and 3’s, you want to assign the ownerships to the person they correspond to. You could do this either one by one, or by using something such as the following for the 3’s (and also for the 1’s and 2’s later):

```
```
chown mary *3
```
```

> **TIP:** Sometimes, you may want to use a metacharacter literally. To accomplish this, put a backslash (\) in front of the metacharacter. Using a backslash in this context makes it an escape character.