# guake

**gnome-terminal** has spawned a couple of programs that reuse many of its internal parts to create different terminal applications. The first is **guake**, a terminal that borrows a design feature from a popular first-person shooter game. When running, *guake* normally hides in the background, when the F12 key is pressed, the terminal window “rolls down” from the top of the screen to reveal itself. This can be handy if terminal is intermittent, or if screen real estate is a premium.

*guake* shares the configuration options with **gnome-terminal**, as well as the ability to configure what key activates it, which side of the screen it rolls from, and its size.

Though *guake* supports tabs, it does not (as of this writing) support profiles. However we can approximate them with a little scripting:

```
#!/bin/bash
# qtab create pseudo-profiles for guake
if [[ $1 == """ ]]; then
  guake --new-tab=. --show
```