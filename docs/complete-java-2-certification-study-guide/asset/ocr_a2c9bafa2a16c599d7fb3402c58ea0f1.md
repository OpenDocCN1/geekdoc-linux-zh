public static void main(String[] args) {

  JFrame frame = new JFrame();

  String[] strings = { "January", "February", "March",

    "April", "May", "June",

    "July", "August", "September",

    "October", "November", "December" };

  StringLengthTableModel model =

  new StringLengthTableModel(strings);

  JTable table = new JTable(model);

  frame.getContentPanePane().add(table);

  frame.setSize(500, 250);

  frame.setVisible(true);

}

On line 24, in getValueAt(), the return value is an int, at first glance is not complete with the return type, which is Object. Line 24 relies on boxing to convert the int to an instance of Integer.

Lines 37 and 38 construct an instance of the model. Line 39 constructs an instance of JTable that uses the new model. Figure 11.14 shows the result.

You can see that the model works, but the size and location in the window are a bit clumsy. That's okay. Chapter 12 will explain how to use layout managers to control the position and location of components.

Often a table contains more data than can fit in the available screen space. In these situations you can put the table inside a JScrollPane, which provides intelligent scrolling for the components. Scrolling a table requires a bit of intelligence because when the user scrolls vertically, you want the table's body to move; the column headers should stay put. Fortunately, JScrollPane knows what should and what should not scroll.

# FIGURE 11.14 A JTable with a custom model

![](bbox=[0.181, 0.706, 0.818, 0.883])