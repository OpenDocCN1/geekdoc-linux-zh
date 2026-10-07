# JRadioButton

Radio buttons are typically used in groups to present exclusive selection. The name comes from the station buttons of older car radios: at any moment, exactly one button is pushed, and pushing in a new button causes the button to pop out. The JRadioButton class is generally used with the ButtonGroup class, which has an add(AbstractButton) method. When a radio button is selected, any other button in the same group is automatically deselected.

The following application creates three radio buttons:

+   1. import java.awt.*;
2. import javax.swing.*;
3.
4. public class RadioDemo {
5.
6.   public static void main(String[] args) {
7.     JFrame frame = new JFrame("Radio Demo");
8.     frame.setSize(350, 250);
9.     Container cont = frame.getContentPane();
10.    cont.setLayout(new FlowLayout());
11.    ButtonGroup btnGroup = new ButtonGroup();
12.    JRadioButton rbtn = new JRadioButton("Rare", true);
13.    btnGroup.add(rbtn);
14.    cont.add(rbtn);
15.    rbtn = new JRadioButton("Medium");
16.    btnGroup.add(rbtn);
17.    cont.add(rbtn);
18.    rbtn = new JRadioButton("Well Done");
19.    btnGroup.add(rbtn);
20.    cont.add(rbtn);
21.    frame.setVisible(true);
22.  }
23. }

Figure 11.9 shows this application's GUI. Because the three radio buttons are added to a button group (lines 13, 16, and 19), they exhibit radio behavior: Selecting one of them causes the previously selected one to become deselected.

Radio buttons, like check boxes, can send Action and Item events. However, as with check boxes, listening for these events is generally not appropriate. A group of radio buttons is often found near an Apply button; the appropriate approach is to read the state of the radio buttons when the user clicks Apply.