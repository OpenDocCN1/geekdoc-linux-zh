# Advanced Bash–Scripting Guide

```
# Note ^[ above is a literal escape
+# typed by Control-V <Esc>

# Bram Moolenaar points out that this may not work with 'vim'
+# because of possible problems with terminal interaction.

exit 0
```

The above could just as effectively have been implemented with ex, rather than vi. Here are documents containing a list of ex commands common enough to form their own category, known as ex scripts.

# Example 17–2, broadcast: Messages to everyone logged in

```
#!/bin/bash

wall <<zzz23EndOfMessagezzz23
E-mail your noctime orders for pizza to the system administrator.
(an extra dollar for anchovy or mushroom topping.)
# Additional message text goes here.
# Note: Comment lines printed by 'wall'.
zzz23EndOfMessagezzz23

# Could have been done more efficiently by
# wall <message-file
# However, saving a template in a script saves works.

exit 0
```

# Example 17–3, Multi-line message using cat

```
#!/bin/bash

# 'echo' is fine for printing single line messages,
# but somewhat problematic for message blocks.
# A 'cat' here denoted overcomes this limitation.

cat <<End-of-message

This is line 1 of the message.
This is line 2 of the message.
This is line 3 of the message.
This is line 4 of the message.
This is the last line of the message.
-----------------------
End-of-message

exit 0
```

```
# Code below disabled, due to "exit 0" above.

# S.C. points out that the following also works.
echo "
-----------------------
This is line 1 of the message.
This is line 2 of the message.
This is line 3 of the message.
This is line 4 of the message.
```

# Chapter 17. Here Documents

237