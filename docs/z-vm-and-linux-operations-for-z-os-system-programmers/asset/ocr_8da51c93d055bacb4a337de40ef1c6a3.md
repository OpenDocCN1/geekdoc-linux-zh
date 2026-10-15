# Table 2-4 Valid areas and output formats for the SCREEN command

| Area or output | Description |
|---|---|
| INAREA | The command line area where you issue commands to CP and guest operating systems. |
| STATAREA | The display of the terminal status at the bottom of the screen. |
| OUTAREA | The area where messages from CP and guest operating systems are placed for you to see. The majority of the screen is this area. |
| CPOUT | This causes all messages from CP to be formatted as specified in the parameters of the command. |
| VMOUT | This causes all messages from a guest operating system to be formatted as specified in the rest of the command. |

Table 2-5 lists the valid effects for the SCREEN command.

# Table 2-5 Valid effects for the SCREEN command

| Effect | Description |
|---|---|
| BLINK | This causes the text on the screen to blink. |
| REVVIDEO | Reverse video swaps the text color and the background color. For example, green text on a black background becomes black text on a green background with the reverse video effect applied. |
| UNDERLIN | This causes the text to be underlined. |
| NONE | This causes no effects to be applied. It prints the text normally in the color specified. |

> Note: To reset your terminal to the default state, use the following SCREEN command:

```
SCREEN ALL DEFAULT
```

# 2.8 Getting started with basic commands for z/VM

This section describes basic commands for navigating in your z/VM system. For more details on the topics discuss here refer to the IBM Redbooks publication, Introduction to the New Mainframe: z/VM Basics, SG24-6366.