```
scanf("%f", &x);
printf("Enter integer y: ");
scanf("%f", &y);
printf("x^y is: %6.3f\n", pow((double)x, (double)y));
}
```

# 3.3.11.1 Practice Session 3.13

Step 1: At the shell prompt, type emacs power.c. Notice that the major mode for this new buffer is set to C/l mode.

Step 2: Type in the program source code exactly as shown. Use the <Tab> key to produce the indentation shown in the C source code. Your emacs screen display should look similar to Figure 3.14.

Step 3: From the pull-down menus, make the choice File>Save (current buffer).

Step 4: From the pull-down menus, make the choice Tools>Compile... In the minibuf-fer, the prompt Compile command: make -k appears. Use the backspace key to erase make -k, and then, to replace it, type cc power.c -lm -o power. A new buffer window appears in the emacs frame, showing the progress of the compilation/linking process.

Step 5: From the pull-down menus, make the choice Tools>Compile... In the minibuf-fer, the prompt Compile command: cc power.c -lm -o power should appear. Press <Enter> to accept this compile/link command.

If you made mistakes in typing the C code, repeat Steps 2 through 5 until you get no error messages that prevent compilation and linkage! The bottom buffer window of

![](bbox=[0.33, 0.7, 0.68, 0.92])