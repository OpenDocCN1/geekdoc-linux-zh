# Layout Policies 431

the positions, gridwidth values, gridheight values, you will see that no component has been placed in, or overlaps, that region.

That's about it for spanning multiple rows and columns. It's not really difficult, although it may have seemed that way before. Now, let's look at a convenient shorthand mechanism for the GridBag layout offers.

# GridBag's Shorthand

You have undoubtedly seen two features used in GridBag layout examples: RELATIVE and REMAIN. These settings provide a shorthand mechanism designed to reduce typing when you're coding a GridBag layout. They can also simplify maintenance of some types of layout.

If you think back to the earlier examples, you will recall seeing many lines setting values for gridx and grid. Very often, the value being set greater by one than the current value; this is often the case in real layouts, too. If you add your components in an orderly fashion, then you will probably set up the component in row zero, column zero first; then do column one, column two; and so on. You could do so using code like:

```
c.gridx++;
```

instead of the explicit name used earlier.

In many cases, if you are filling a layout completely, from top-left to bottom-right, one row at a time, then the shorthand mechanism of RELATIVE and REMAINDER will help. Let's look at a simple example:

```
import java.awt.*;
import javax.swing.*;

public class Shorthand extends JPanel {
    setLayout(new GridBagLayout());
    GridBagConstraints c = new GridBagConstraints();
    c.fill = GridBagConstraints.BOTH;
    c.weightx = 1;

    add(new JButton('1'), c);
    add(new JButton('2'), c);
    add(new JButton('3'), c);
    add(new JButton('4'), c);
    c.gridwidth = GridBagConstraints.REMAINDER;
    add(new JButton('5'), c);
    c.gridwidth = 1;
    c.weightx = 0;

    add(new JButton('A'), c);
    add(new JButton('B'), c);
```