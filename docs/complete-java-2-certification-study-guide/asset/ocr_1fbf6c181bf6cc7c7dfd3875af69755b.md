# Chapter 12 · Layout Managers

The first four of these methods are straightforward; first and last cause the display to select the first or last added component, respectively. Similarly, the methods next and previous cause the displayed component to be cycled based on the order in which the components were originally added to the container.

The final method, show(), selects a particular component based on the textual name that was given to the component when it was added to the container. To use this method, naturally, you must provide a name for the component. You do so by using the method add(Component, Object)

to add the component to its container and ensuring that the names given to the components are unique for that container.
Let's look at an example. Especially the underlined lines, where components are added and displayed:

```
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
```

```
public class CardDemo extends JPanel {
    private JPanel cardPanel = new JPanel();
    private BorderLayout cardLayout = new BorderLayout();

    private JPanel controlPanel = new JPanel();

    private JButton firstName = new JButton("First");
    private JButton lastName = new JButton("Last");
    private JButton nextButton = new JButton("Next");
    private JButton prevButton = new JButton("Prev");
    private JTextField selectText = new JTextField("*"); }
```

```
public CardDemo() {
    setLayout(new BorderLayout());
```

```
cardPanel.setLayout(cardLayout);

JPanel p = new JPanel();
p.setLayout(new BorderLayout());
p.add(new Label("This is panel One"),
    BorderLayout.CENTER);
p.add(new Button("dummy button one"),
```