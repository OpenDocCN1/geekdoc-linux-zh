# Capname

# Description

rmso | End “standout” mode
sgr0 | Turn off all attributes
setaf <value> | Set foreground color
set <value> | Set background color

# Text effects capnames

Some capabilities, such as underline and standout, have capnames to turn the attribute both on and off while others only have a capname to turn the attribute on. In these cases, the sgr0 capname can be used to return the text rendering to a “normal” state. Here is a simple script that demonstrates the common text effects:

```
#!/bin/bash
# tput_characters - Test various character attributes
clear
echo "tput character test"
echo "======================"
echo
tput bold; echo "This text has the bold attribute."; tput sgr0
tput smul; echo "This text is underlined (smul);"; tput rmul
# Most terminal emulators do not support blinking text (though xterm
# does) because blinking text is considered to be in bad taste ;-)
tput blink; echo "This text is blinking (blink)."; tput sgr0
tput rev; echo "This text has the reverse attribute"; tput sgr0
# Standout mode is reverse on many terminals, bold on others.
tput smso; echo "This text is in standout mode (smso)."; tput rmso

tput sgr0
echo
```