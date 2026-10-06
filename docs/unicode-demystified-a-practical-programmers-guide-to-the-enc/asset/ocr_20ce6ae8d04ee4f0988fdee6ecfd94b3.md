```
while ((*dest++ = *source++)) != '\0'
  /* void loop body */
  return (dest - 1);
```

+   a. What command moves the cursor to the opening brace of strcpy? What command moves the cursor past the closing brace? Can you use these commands to skip through the buffer in one-procedure steps?

+   b. Assume the cursor is just past the closing parenthesis of the while condition. How do you move to the matching opening parenthesis? How do you move back to the matching close parenthesis again? Does the same command set work for matched [] and {}? How does this differ from the vi % command?

+   c. One procedure is indented in the Berkeley indention style; the other is indented in the GNU style. What command reindents a line in accordance with the current indention style you have set up? How would you reindent an entire procedure?

+   d. Suppose that you want to write five string procedures and intend to use strcpy as a starting point for further editing. How would you make five duplicate copies of the strcpy procedure?

+   e. How would you compile the code without leaving emacs?