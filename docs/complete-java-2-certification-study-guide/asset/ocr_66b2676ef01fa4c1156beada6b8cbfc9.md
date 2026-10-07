```
59. 0, 10, 0, 100), c;
60.
61. c.gridx = 2; c.gridy = 4;
62. c.gridwidth = 1;
63. c.gridheight = 1;
64. add(new JScrollBar(JScrollBar.HORIZONTAL,
65. 0, 10, 0, 100), c);
66.
67. c.gridx = 3; c.gridy = 4;
68. c.gridwidth = 1;
69. c.gridheight = 1;
70. add(new JScrollBar(JScrollBar.HORIZONTAL,
71. 0, 10, 0, 100), c);
72.
73. }
74.
75. public static void main(String[] args) {
76. JFrame f = new JFrame("GridBag Example 4");
77. f.getContentPane().add(new cellSize(),
BorderLayout.CENTER);
78. f.pack();
79. f.setVisible(true);
80. }
```

Notice that line 11 the fill value has been set to BOTH and is left at this setting for all uses of the GridBagConstraints object. As a result, all columns will be stretched to fill these cells; this is the case even if the cells extend over multiple rows or columns. This way, you can see more easily where the boundaries of the cells are.

The next point about this code is that it is considerably longer than it needs to be. For every-
ponent that is added, the settings of gridx, gridy, gridwidth, and gridheight are explicitly set before the after(add) method is called. This makes it easier to see how each value is set without having to scan up and down to there.

Compare the code with the screen shot in Figure 12.33. You will see the correspondence
bween gridwidth and the number of columns of a component spans, and between gridheight
 the number of rows for a component spans. For example, the right button at the top of the lay-
out is created by lines 17–20. At line 18, gridwidth is set to 3, and Figure 12.33nshows that the button extends across three columns.
Similarly, the large central button is set up by lines 28–31. Notice that the gridwidth and
height values are set to 2. Figure 12.33 shows that the button is two columns wide and
row rows high.

One aspect warrants mention. At row 3, column 2, there is a blank space. This is per-ectly acceptable, although it is unlikely to happen in a real GUI layout. If you work through all