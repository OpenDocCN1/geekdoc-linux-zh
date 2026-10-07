Add the following code snippets to the Prototype class as a way to experiment, and compare
y perception of speed before and after these changes. The dialogs that pop up are depicted in
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

![](bbox=[0.246, 0.387, 0.773, 0.496])

a

b

# Summary

A simple, four-step plan to design a GUI identifying the needed components, isolating
regions of behavior, sketching the GUI, and choosing layout managers.
Some properties are common to nearly all Swing components. These include size, location,
foreground and background color, font, and enabled state. There are public methods for each
component to set and get each of these properties.

The categories of Swing components are container components, ordinary components,
and menu components. Components include JFrame, JPanel, and JPane. Ordinary components
include JLabel, JButton, JCheckBox, JRadioButton, JScrollPane, JTextField,
JTextArea, and JComboBox. The menu components include JMenu, JMenuBar, JMenuItem,
JCheckBoxMenuItem, and JRadioButtonMenuItem.

JTables have three core internal models, using TableModel, TableColumnModel,
and ListenerSelectionModel. It's also possible (or simpler) to subclass AbstractTableModel
and use it as a JTable constructor argument.

The primary use for a JTree is implementing a data structure that lends to a hierarch-
chy. Trees consist of a root node and child nodes (leaf nodes and branch nodes).