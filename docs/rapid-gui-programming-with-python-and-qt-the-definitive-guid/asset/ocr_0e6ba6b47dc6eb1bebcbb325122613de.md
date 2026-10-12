just like a tab widget, and additional options for navigating between pages and for changing the page order.

Since stacked widgets have no tabs, we must provide the user with a means of navigating between pages. In the VehicleRentalDlg shown in Figure 9.2, the vehicle type combo box is used as a page selector. To make this work, in Qt Designer we have connected the combo box's currentIndexChanged(int) signal to the stacked widget's setCurrentIndex(int) slot. Another commonly used approach that lets users see all the pages available is to use a QListWidget containing the name of each page, and connecting its currentRowChanged(int) signal in the same way we connected the combo box's signal.

We will now see how to create a stacked widget in code. The following extracts are from the VehicleRentalDlg class's initializer in chapp9/vehiclerentaldlg.ppy. (The Qt Designer version is in the files vehiclerentaldlg.ui and vehiclerentaldlg.py.)

```
self.stackedWidget = QStackedWidget() 

carWidget = QWidget() 

carLayout = QGridLayout() 

carLayout.addWidget(colorLabel, 0, 0) 

carLayout.addWidget(self.colorComboBox, 0, 1) 

carLayout.addWidget(seatsLabel, 1, 0) 

carLayout.addWidget(self.seatsSpinBox, 1, 1) 

carWidget.setLayout(carLayout) 

self.stackedWidget.addWidget(carWidget)
```

Adding a “page” to a stacked widget is very similar to adding a tab to a tab widget. We begin by creating a plain widget, and then create a layout for it and lay out the widgets we want. Then we set the layout on the plain widget and add this widget to the widget stack. We have not shown the code for the vanWidget, because it is structurally identical.

```
topLayout = QVBoxLayout() 

topLayout.addWidget(vehicleLabel) 

topLayout.addWidget(self.vehicleComboBox) 

bottomLayout = QVBoxLayout() 

bottomLayout.addWidget(mileageLabel) 

bottomLayout.addWidget(self.mileageLabel) 

layout = QVBoxLayout() 

layout.addLayout(topLayout) 

layout.addWidget(self.stackedWidget) 

layout.addLayout(bottomLayout) 

layout.addWidget(self.buttonBox) 

self.setLayout(layout)
```

Once again, for completeness we have shown the whole dialog's layout. We begin with a top layout that has the combo box that is used to set the stacked