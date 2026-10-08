# Getting onto the System and Using the Command Line

![](bbox=[0.128, 0.143, 0.198, 0.168])

+   1. To use the infix calculator, enter the following command:

% bc
Nothing happens—prompt, nothing. The reason is that bc, like its RPN cousin, waits for you to enter commands. The quit command lets you leave the program. You can see how it works by seeing how I solve the first and second mathematical equations of Table 2.1:
% bc
75 * 0.85
63.75
(37*1.334)+44
93.358
quit

+   2. Unfortunately, bc is, in many ways, a typical UNIX command. Consider what happens when I enter help, hoping for some clue on how to use the bc program:

% bc
help
syntax error on line 1, totype

+   3. This is not very helpful. If you get stuck in a command, there are two sure ways to escape. Control-a (holding down the Control—also called Ctrl—key on your keyboard and simultaneously pressing the a key) indicates that you have no further input, which often causes programs to quit. If that fails, Control-e kills the program, that forces it to quit immediately.
The bc command has a number of powerful and useful options, as shown in Table 2.2.

# Table 2.2. Helpful bc commands.

| Notation | Description of Function |
|---|---|
| sqrt(n) | Square root of n |
| % | Remainder |
| ^ | To the power of (3^5 is 3 to the power of 5) |
| s(n) | Sine(n) |
| c(n) | Cosine(n) |
| e(n) | Exponential(n) |
| l(n) | Log(n) |