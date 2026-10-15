# Working with a 3270 terminal

Previously, we explained how to log on to the z/VM system, and you saw the response from the system. Now we discuss what you have to know when working with a 3270 terminal on a z/VM system.

Figure 2-15 shows the layout of the 3270 window.

![](bbox=[0.26, 0.26, 0.88, 0.66])

Figure 2-15 Layout of the 3270 window

The three areas of the window are: Output display area, User input area, and Screen status area, as described in Table 2-1.

Table 2-1 Display areas

| Area | Description |
|---|---|
| Output display area | - Consists of lines 1 to 22.
- All messages are displayed here.
- The commands you entered are displayed here. |
| User input area | - Consists of last two lines, excluding the right-most 21 character positions of the last line.
- Commands can be entered here.
- Cursor control keys, Delete key, Insert Key and logical text editing characters can be used to alter data in this area.
- After pressing Enter, CP redisplays the data entered here in the output display area. |