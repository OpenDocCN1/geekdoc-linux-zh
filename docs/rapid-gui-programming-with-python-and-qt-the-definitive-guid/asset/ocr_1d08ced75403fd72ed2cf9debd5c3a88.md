```
self.emit (SIGNAL(" clicked (QModelIndex)"),
            self.model.index(self.selectedRow, 0))
        else:
            QWidget.keyPressEvent(self, event)
```

We have chosen to support just two key presses: Up Arrow and Down Arrow. If the user presses either of these, we increment or decrement the selected row, make sure that the selected row is in range, and then schedule a paint event.

If the user navigates to the row above the topmost visible row or below the bottommost visible row, we tell the scroll area to make sure that the row that has been scrolled to is visible—if necessary, the scroll area will scroll to achieve this. We also emit a clicked() signal with the newly selected row’s model index. It is quite conventional to use a clicked() signal in this circumstance, since in effect, the user is “clicking” using the keyboard—after all, the signals and slots mechanism is concerned with what the user wants rather than how they asked for it, and here they just want to select a row.

If we do not handle the key press ourselves, that is, for all other key presses, we pass the event on to the base class.

The water quality view widget is visually very different from the table view shown beside it, yet it did not require that much code to implement and was not too difficult to program. We made the widget fairly efficient by reducing the amount of unnecessary painting. We also made the painting code as simple as possible by ensuring that the widget was always exactly the size necessary to display the entire dataset. The disadvantage of this approach is that it pushes responsibility on to the programmer using our widget to use a QScrollArea, although this saves us from having to implement scrolling ourselves.

The water quality view visualizes the data in one-to-one correspondence with the data in the model, but we are not constrained to doing this. It is also possible to create custom views that show aggregated data. In this case, for example, we could have shown one entry per day, or per hour, perhaps by averaging each day or hour’s readings.

# Generic Delegates

As we have seen in earlier chapters, custom delegates allow us to exercise complete control over the appearance and behavior of the data items that appear in views. Although it is obvious that if we have many models, we are likely to want a custom delegate for most if not all of them, what is not so obvious, is that the custom delegates will very likely have a lot of duplicate code.*

*This section is partly based on ideas from the author’s whitepaper, “Qt 4’s Model/View Delegates”, available at http://www.ics.com/developers/papers/f.