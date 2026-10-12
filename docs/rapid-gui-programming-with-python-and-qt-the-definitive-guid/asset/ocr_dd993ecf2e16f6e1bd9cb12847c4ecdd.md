user can navigate between pages. Tab widgets can have rounded or angled tab corners, and can have the tabs at the top, bottom, left, or right.

Although using *Qt Designer* is quicker and easier than creating the dialog by hand, it is interesting and useful to know how to achieve the same thing purely in code. We won’t show the creation of the ordinary widgets, since we have seen that enough times by now; instead, we will focus on the tab widget and the form’s overall layout. The following extracts are all from the PaymentDlg class’s initializer in chap09/paymentdlg.pyw. (The *Qt Designer* version is in the files paymentdlg.ui and paymentdlg.py.)

```
tabWidget = QTabWidget()
cashWidget = QWidget()
cashLayout = QBoxLayout()
cashLayout.addWidget(self, paidCheckBox)
cashWidget.setLayout(cashLayout)
tabWidget.addTab(cashWidget, "Cas$h")
```

We create the tab widget just like any other widget. Each page in a tab widget must contain a widget, so we create a new widget, *cashWidget*, and create a layout for it. Then we add the relevant widgets—in this case, just one, *paidCheckBox*—to the layout, and then set the layout on the containing widget. Finally, we add the containing widget as a new tab to the tab widget, along with the tab’s label text.\*

```
checkWidget = QWidget()
checkLayout = QGridLayout()
checkLayout.addWidget(checkNumLabel, 0, 0)
checkLayout.addWidget(self.checkNumLineEdit, 0, 1)
checkLayout.addWidget(bankLabel, 0, 2)
checkLayout.addWidget(self.bankLineEdit, 0, 3)
checkLayout.addWidget(accountNumLabel, 1, 0)
checkLayout.addWidget(self.accountNumLineEdit, 1, 1)
checkLayout.addWidget(sortCodeLabel, 1, 2)
checkLayout.addWidget(self.sortCodeLineEdit, 1, 3)
checkWidget.setLayout(checkLayout)
tabWidget.addTab(checkWidget, "Check$")
```

This tab is created in exactly the same way as the first one. The only differences are that we have used a grid layout, and we have more widgets to put in the layout.

We won’t show the code for the third tab, because it is structurally the same as the ones we have already seen.

\*In the PyQt documentation, and to some extent, the Qt\*bWidget’s API, the term “tab” is used to refer to a tab’s label alone, and to a tab’s label and page together.