# Advanced Bash-Scripting Guide

Note that single quotes enclose the remainder of the command sequence following the echo -e.
The numbers in the following table work for an rxvt terminal. Results may vary for other emulators.

# Table 36-1. Numbers representing colors in Escape Sequences

| Color | Foreground | Background |
|---|---|--|
| black | 30 | 40 |
| red | 31 | 41 |
| green | 32 | 42 |
| yellow | 33 | 43 |
| blue | 34 | 44 |
| magenta | 35 | 45 |
| cyan | 36 | 46 |
| white | 37 | 47 |

# Example 36-15. Echoing colored text

```
#!/bin/bash
# color-echo.sh: Echoing text messages in color.

# Modify this script for your own purposes.
# It's easier than hand-coding color.

black='\E[30;47m'
red='\E[31;47m'
green='\E[32;47m'
yellow='\E[33;47m'
blue='\E[34;47m'
magenta='\E[35;47m'
cyan='\E[36;47m'
white='\E[37;47m'
```

```
alias Reset="tput sgr0"
# Wait, looking at the image text again:
alias Reset="tput sgr0" # Reset text attributes to normal
  # without clearing screen.

cecho () {
  # Color-echo.
  # Argument $1 = message
  # Argument $2 = color
  local default_msg="No message passed."
  # Doesn't really need to be a local variable.

  message=${1:-default_msg} # Defaults to default message.
  color=${2:-black} # Defaults to black, if not specified.

  echo -e "$color"
  echo "$message" # Reset to normal.

  return
}
```

Chapter 36. Miscellany