| Name | Description |
|---|---|
| Hover Click | Mouse option that triggers a mouse click when the pointer is hovered over an item. |
| Mouse Keys | Mouse option that allows you to use keyboard keys to emulate the mouse functions. |
| Repeat Keys | Keyboard option that modifies how long a key must be pressed down as well as a delay to acknowledge the key repeat. Also called keyboard repeat rate. |
| Screen Keyboard | Keyboard option that displays a visual keyboard on the UI that can be manipulated by a mouse or other pointing device to emulate key strokes. |
| Simulated Secondary Click | Mouse option that sets a primary key to be pressed along with a mouse click to emulate secondary mouse clicks. |
| Slow Keys | Keyboard option that modifies how long a key must be pressed down to acknowledge the key. |
| Sticky Keys | Keyboard option that sets keyboard modifier keys, such as Ctrl and Shift, to maintain their pressed status until a subsequent key is pressed. |

AccessX was a program that provided many of the options in Table 8.6. Thus, you will often see it referred to in the accessibility control panels, such as in the Typing Assist (AccessX) option. One interesting AccessX setting is Enable By Keyboard, which allows you to turn on or off accessibility settings via keystrokes on the keyboard.

# # Serving Up the GUI

Many players are involved in providing a Linux system user interface. The desktop environment components are only a piece of this puzzle. Figure 8.6 is a rudimentary depiction of serving a GUI to a user.

In Figure 8.6, notice that the window manager is an intermediary in this scenario. A window manager is a program that communicates with the display server (sometimes called a window manager) on behalf of the UI. Each particular desktop environment has its own default window manager, such as Mutter, Kwin, Muffin, Marco, and Metacity.

In the following sections, we will focus on the display server, a program that uses a communication protocol to transmit the desires of the UI to the operating system, and vice versa. The communication protocol is called the display server protocol and can operate over a network.