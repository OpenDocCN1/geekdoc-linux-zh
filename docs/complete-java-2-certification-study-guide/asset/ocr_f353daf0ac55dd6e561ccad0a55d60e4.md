# Controlling Component Position and Stretch in a Cell

You saw in the previous example that a component that occupies an oversized cell is normally placed in the center of the space, at its preferred size. Both of these features are controllable. Using a feature called anchor, you can control where the component is placed within its available space. Using a feature called fill, you can determine whether a component stretches to fill the available space, either horizontally, vertically, or both. Let's look at several examples. We will start with this code:

```
1. import java.awt.*;
2. import java.awt.event.*;
3. import javax.swing.swing.*;
4.
5. public class GB2 extends JPanel (
6.   public Font bigfont = new Font("Serif", Font.PLAIN, 36);
7.   setLayout(new GridBagLayout());
8.   GridBagConstraints c = new GridBagConstraints();
9.
10.
11.  c.gridx = 0; c.gridy = 0;
12.  addButton('TL', bigfont, c);
13.  c.gridx = 1;
14.  addButton('Top Middle', bigfont, c);
15.  c.gridx = 2;
16.  addButton('TR', bigfont, c);
17.
18.  c.gridx = 0; c.gridy = 1;
19.  addButton('ML', bigfont, c);
20.  c.gridx = 2; // not skipped over x=1, y=1
21.  addButton('MR', bigfont, c);
22.
23.  c.gridx = 0; c.gridy = 2;
24.  addButton('BL', bigfont, c);
25.  c.gridx = 1;
26.  addButton('Bottom Middle', bigfont, c);
27.  c.gridx = 2;
28.  addButton('BR', bigfont, c);
29.
30.  Font smallfont = new Font("SansSerif", Font.PLAIN, 10);
31.  c.gridx = 1; c.gridy = 1;
32.  addButton('x', smallfont, c);
```