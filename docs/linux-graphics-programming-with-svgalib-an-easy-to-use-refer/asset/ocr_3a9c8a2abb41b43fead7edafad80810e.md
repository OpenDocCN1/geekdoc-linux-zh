actually developed in the early 1960s by someone named Doug Engelbart. Furthermore, it's fairly well known now that Apple (the “Linus of the “80s”) didn't help to develop the mouse (as it appeared at the time). Instead, Apple stole it from Xerox, along with the GUI. I'm not a complete Apple basher, though Apple certainly helped to popularize both mice and GUIs, and Apple/OS Basic will always have a special place in my heart—even if it was written by Microsoft (cough, cough).

# Customizing libvga.config

Moving right along, the mouse is defined in `/etc/vga/libvga.config`. It's possible to pass all mouse parameters to the program at execution time (thus eliminating the need for the mouse section of libvga.config), but you must be aware that most programs don't do this. Therefore, you'll need to work with this onerous file once again.

Fortunately, what you're interested in appears right on top:

```
```text
# Mouse type:
# mouse Microsoft # Microsoft
# mouse MouseSystems # Mouse Systems
# mouse MMSeries # Logitech NM Series
# mouse Logitech # Logitech protocol
# mouse Bsmouse # Bus mouse
# mouse PS2 # PS/2 mouse
# mouse MouseMan # Logitech MouseMan
# mouse Spaceball # Spacejet SpaceBall
# mouse IntelliMouse # Microsoft IntelliMouse
# or Logitech MouseMan+ on
# serial port.
# mouse IMPS2 # Microsoft IntelliMouse
# or Logitech MouseMan+ on
# PS/2 port.
# mouse none # None
mouse none
```

```

The mouse section first contains sample definitions (commented out with hash marks) and then the actual configuration. Note that I have mine set as “mouse none”. To install a Microsoft mouse, you would change this to the following:

```
```text
mouse Microsoft
```

```

I'm sure you can figure out what to do if, for example, you have a Logitech mouse.

> **Note**
> Did you know that the “proper” term for the hash or pound sign (#) is octothorpe?