
Other properties of JSplitPane include

- orientation HORIZONTAL_SPLIT or VERTICAL_SPLIT
- dividerSize In pixels
- dividerLocation Current position
- minimumDividerLocation Left/bottom minimum size
- maximumDividerLocation Right/top minimum size

Now you're ready to put the tree, and simple menu together for a first look, which you can create with the following code:

```
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
import javax.swing.tree.*;

/** A bootstrap class that combines our table and tree,
 * in a split pane, along with a trivial menu that is
 * backed by an Action.
 * @Author The CJ2CSG Guys
 */
public class Prototype {

    public static void main(String[] args) {
        JFrame jf = new JFrame('SplitPane Test');

        TroubleTicketModel ttm = new TroubleTicketModel();
        JTable jta = new JTable(ttm);

        SampleTree st = new SampleTree('sample');
        DefaultTreeModel tm = st.getTreeModel();
        JTree jtr = new JTree(tm);

        SampleAction sa = new SampleAction('PROTOTYPE');
        JMenuBar jmb = new JMenuBar();
        jf.setJMenuBar(jmb);
        JMenu jm = new JMenu('Sample');
        jmb.add(jm);
        jm.add(sa);
```

Panes 391

```
JSplitPane jsp = new
JSplitPane(JSplitPane.HORIZON_SPLIT, jtr, jta);
```

```
jf.getContentPane().add(jsp, BorderLayout.WEST);
jf.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
jf.setSize(650,200);
jf.setVisible(true);
}
```

The result is shown in Figure 11.20. You didn't spend time refining appearances in this round, but now you have a quick look at your elements. Most of the adjustments to appearance can be made in the bootstrap code, amounting to less focus on changing class behavior and more on experimenting with it.

# Figure 11.20 Menu, table, and tree together in one JFrame

![](img/09f8389b7ae2705d1ab14be2d5e857e3_425_0.png)

# JOptionPane

The JOptionPane class encapsulates several conventional dialog-box formats, but with one clear advantage: You don't need to declare a Frame and bind to it (more than that in a moment). JOptionPane defines five message types:

- ERROR_MESSAGE
- INFORMATION_MESSAGE
- WARNING_MESSAGE
- QUESTION_MESSAGE
- PLAIN_MESSAGE

Each of these types maps to a prepared display format. These formats can be associated in two ways: using a confirmation request that locks the underlying frame (a modal dialog) or using a dismiss-on-demand style that does not interfere with the application (a nonmodal dialog). These behaviors are respectively enabled by the static methods showConfirmDialog() and showDialog().

Add the following code snippets to the Prototype class as a way to experiment, and compare y perception of speed before and after these changes. The dialogs that pop up are depicted in
Figure 11.21:

```
JOptionPane.showMessageDialog(null, "Tree created",
"Program Note", JOptionPane.INFORMATION_MESSAGE);
```

```
JOptionPane.showConfirmDialog(null, "Load the GUI?",
"Roll Call!", JOptionPane.YES_NO_CANCEL_OPTION,
JOptionPane.QUESTION_MESSAGE);
```

...

# FIGURE 11.21 JJOptionPane's information (a) and question (b) dialogs

![](img/09f8389b7ae2705d1ab14be2d5e857e3_426_0.png)

a

b

# Summary

A simple, four-step plan to design a GUI identifying the needed components, isolating
regions of behavior, sketching the GUI, and choosing layout managers.
Some properties are common to nearly all Swing components. These include size, location,
foreground and background color, font, and enabled state. There are public methods for each
component to set and get each of these properties.

The categories of Swing components are container components, ordinary components,
and menu components. Components include JFrame, JPanel, and JPane. Ordinary components include JLabel, JButton, JCheckBox, JRadioButton, JScrollPane, JTextField,
JTextArea, and JComboBox. The menu components include JMenu, JMenuBar, JMenuItem, JCheckBoxMenuItem, and JRadioButtonMenuItem.

JTables have three core internal models, using TableModel, TableColumnModel,
and ListenerSelectionModel. It's also possible (or simpler) to subclass AbstractTableModel
and use it as a JTable constructor argument.

The primary use for a JTree is implementing a data structure that lends to a hierarch-chy. Trees consist of a root node and child nodes (leaf nodes and branch nodes).

# Chapter Review Lab

# A Custom Table Model Class

In this exercise you will create your own table model class. The model should support a table with 10 rows and 10 columns. The cell at row r and column c should display the value r × c. In other words, it's a multiplication table for 0 times through 9 times. The column headers should be the values 0 through 9. A good size for your frame is 800 × 200 pixels.

The cells in the rightmost column and the bottom row should be blank. If you're not familiar with layout managers, you might run into problem. The GUI should display the and add to the frame. If you test the application, be sure to the last value. One possible solution appears in the file MultiplicationTableModel.java. Your class should also implement ActionListener, so that it can receive notification from the. When you type into the last cell, insert the following line of code immediately after you create the:

```
frame.getContentPane().setLayout(new java.awt.FlowLayout());
```

# Chapter 12

# Layout Managers

![](img/09f8389b7ae2705d1ab14be2d5e857e3_429_0.png)
