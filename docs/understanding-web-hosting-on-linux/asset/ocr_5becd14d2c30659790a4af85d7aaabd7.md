# 82 · CHAPTER 6

![](bbox=[0.315, 0.075, 0.835, 0.405])

# Text Fields

Of the input types in Figure 6.7, the text field is the easiest to describe:

```
<INPUT TYPE="text" NAME="name" SIZE=25 MAXLENGTH=25>
```

The TYPE option declares the input as text; NAME creates what amounts to a variable name; SIZE declares the number of characters viewable on the browser panel; and MAXLENGTH declares the maximum number of characters that can be entered in that text field. Notice the prompt for the input field. <B>Name:</B> <B>/B> tags just signify bold.

# Check Boxes

The first check box in Figure 6.7 defines the input field as a check box with a variable name of RPG:

```
<INPUT TYPE="checkbox" NAME="name" VALUE="RPG">RPG
```

Unlike the text, the checkbox has its value explicitly specified as "RPG". Check boxes are Boolean values. In this example, a user clicks it to indicate that he or has RPG programming experience. If the user does not click the check box, the RPG input field isn't even sent to the server. If the user clicks the check box, the input field identified with the variable name of RPG is sent to the server with the value of "RPG".