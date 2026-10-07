It seems that line 10 would force the buttons to be 300 pixels wide by 300 pixels. In fact, the buttons are just the size they would be if line 10 were omitted or commented out.
Line 10 has no effect after it executes, the button is added to a panel (line 11). Eventually (after a fairly complicated sequence of events), the panel calls on its layout manager to enforce its layout policy on the button. The layout manager decides where and how big the button should be; in this case, the layout manager wants the button to be large enough to accommodate its label. When this size has been calculated, the layout manager calls setBounds() on the button, clobbering the work you did in line 10.
In general, it is futile to call set() on a component, because layout managers always get the last word; that is, their call to setBounds happens after yours. There are ways to defeat this functionality, but they tend to be complicated, difficult to maintain, and not in the spirit of Java. Java's GUI system wants you to let the layout managers do the work. In order to build a sophisticated GUI, you have to be familiar with the layout policies of the available layout managers. These policies are covered in the next several sections.

# Layout Policies

# The Layout Manager

The Flow manager arranges components in horizontal rows. It is the default manager for panels and applets, so it is the first layout manager that programmers encounter. It is a common experience for new Java developers to add few components to the applet and wonder how they come to be arranged neatly. The following code is good example:

+   1. import java.awt.*;
2. import javax.swing.*;
3.
4. public class Flow extends JFrame {
5. public static void main(String[] args) {