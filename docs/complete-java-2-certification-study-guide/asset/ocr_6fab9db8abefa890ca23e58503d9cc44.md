# Basic Swing Components 373

```
class BarListener implements AdjustmentListener {
  public void adjustmentValueChanged(AdjustmentEvent e) {
    System.out.println("Val = " + e.getValue());
  }
}
```

Scroll bars send events to registered Adjustment listeners. In this example, the listener is an instance of the BarListener inner class. The ScrollDemo application produces the GUI shown in Figure 11.10.

# FIGURE 11.10 JScrollBar example

![](bbox=[0.198, 0.347, 0.476, 0.513])

# J JTextField and JTextArea

J JTextField and JTextArea components support single-line and multiline text entry. Both classes extend javax.swing.text.JComponent, which provides methods for accessing and modifying the component's text. The API page for JComponent includes a good description of text functionality.

Both JTextField and JTextArea send events when they receive keyboard input. In addition, JTextField sends Action events when the user presses Enter. The following application contains one of each component; the JTextArea displays information about events in the JTextField. Once again, the Flow layout manager is inappropriate for the components we want to demonstrate, so we use a Border layout:

```
import java.awt.*;
import java.awt.event.*;
import javax.swing.*;
```

```
public class TextDemo extends JFrame
  implements ActionListener, KeyListener {
  private JTextField field;
```