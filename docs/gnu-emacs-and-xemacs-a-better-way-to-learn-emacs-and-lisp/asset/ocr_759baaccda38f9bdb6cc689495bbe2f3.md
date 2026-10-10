![](bbox=[0.07, 0.08, 0.93, 0.5])

**Figure 16.7  *JDE’s Autocode Group***

After it’s evaluated, pressing M-x and typing

tempo-template-hello

causes this string to be inserted in the current buffer at point:

```
System.out.println("hello");
```

Notice the backslash escape characters in the Lisp statement just shown. They are necessary, because the quoted string "hello" needs to be preserved from unwanted Lisp interpretation.

Now take a look at Figure 16.8. Notice the INS and DEL buttons to the left of each item. To add the "hello" template to the buffer, you click on the INS button at the bottom of the Code Templates category and fill in the name of the template and the command used to invoke it.

Make sure you save your changes by clicking on the State button. The next time you use JDE, you should be able to insert your new template with a menu selection.

JDE is one of the largest and most complex packages available for Emacs. Several chapters would be required to really do it justice. More background and installa-