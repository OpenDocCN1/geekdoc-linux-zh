In addition to the width problem, this dialog now has a height problem. The text field has become taller, but the font hasn't grown. The text looks lost and forlorn in the middle of all that white background.

As a general principle, it isn't enough to think about the size of a component at the moment it is displayed. You need to consider the consequences of resizing. In our example, a more sophisticated layout scheme is called for:

```
JDialog dialog = new JDialog();
Container cont = dialog.getContentPane();
cont.setLayout(new GridBagLayout());
GridBagConstraints gbc = new GridBagConstraints();
gbc.gridx = 0;
gbc.gridy = 0;
gbc.gridwidth = 1;
gbc.gridheight = 1;
gbc.weightx = 0;
cont.add(new JLabel("*")
```

Now even in its initial appearance the label's width is appropriate, as seen in Figure 14.4.
When the dialog resizes, the components stay the right, as seen in Figure 14.5.

# FIGURE 14.4 Appropriate component size

![](bbox=[0.243, 0.636, 0.363, 0.673])

# FIGURE 14.5 Appropriate component size, after resizing

![](bbox=[0.243, 0.745, 0.643, 0.836])