When prompted, respond tersely with

The resultant Customize buffer will look something like Figure 16.3.

# Possible Performance Problems

When you use the navigation key commands to jump from the body of a statement back to the beginning, or from a preprocessor conditional to the previous one, quite a bit of scanning and parsing are going on behind the scenes. With some coding styles, cc-mode can get lost and stalled, possibly even hanging the Emacs session. cc-mode prefers to scan forward in a file, because C and C++ can be difficult for the mode to interpret when moving backward, against the logical flow. The mode makes a leap backward, hoping to overshoot, say, the beginning of a function, and then scans forward until it is found.

There is an easy way to avoid these potential problems: Try to place the opening curly brace that begins a function definition (in C) or class definition (in C++ or Java) in the first column. Emacs and cc-mode try to encourage this by the way indentation and electric characters are set up.

![](bbox=[0.18, 0.06, 0.84, 0.43])