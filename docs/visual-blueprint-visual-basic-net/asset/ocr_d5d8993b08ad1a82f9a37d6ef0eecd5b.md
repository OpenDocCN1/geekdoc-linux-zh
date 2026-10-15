# USING THE PRINTER DIALOG BOX

Before an application prints, it often presents a Printer selection dialog box to let the user select which printer to use and any printer driver options, such as draft mode. You can add the Print dialog box to your application using the PrintDialog control.

The PrintDialog control is available in the Windows Form section of the Toolbox. A required property for the function of the PrintDialog control is Document. You must set this property to a valid Document provided by a PrintDocument control.

Other than the Document property, you can edit properties to determine what functions to make available to the user. AllowPrintToFile enables or disables the "Print To File" checkbox. If AllowPrintToFile is True and the user checks the box, the PrintToFile property is set to True. AllowSelection enables or disables the range selector boxes, which enable the user to print only a particular range of pages. AllowSomePages enables or disables the box where the user can enter a selection of pages either individually or by range. If you enable these properties, the PrintDocument control manages the correct pages to print.

To make the dialog box appear, invoke the ShowDialog method with no arguments. The method returns a DialogResult specifying either OK or Cancel. For more information on DialogResult, see Chapter 3. If the user clicks OK, the PrinterDialog sets the dialog box settings to the PrinterSettings of the PrintDocument component. If you call the ShowDialog method and the user does not have any defined printers, a message appears notifying the user how to add a printer and the DialogResult returns Cancel. You can use the Reset method to clear any previous settings the user has made and reset the dialog box to defaults.

The example uses a Button control to activate the Print dialog box. You can use a variety of controls such as a toolbar or menu as well.

![](bbox=[0.04, 0.56, 0.96, 0.78])

+   1. Open a form in a Windows Application project.
+   2. Add and configure a PrintDocument component on the form.

> Note: See the section "Using the PrintDocument Control" to add a PrintDocument to the form.

+   3. In the Toolbox, double-click the PrintDialog control to add it to the form.
+   The control appears in the Component Tray.

+   4. In the Properties window, click the Document and select PrintDocument control.
+   You can optionally set other properties and toggle preference properties like AllowSelection by double-clicking the property name.

+   5. Open the method or event where the Printer dialog box needs to appear.