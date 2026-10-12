
# Designing the interface

numbers are on display.

- One Button widget to clear the numbers on display in the Label widgets when this Button gets clicked. This Button will not be enabled when the numbers are not on display.

Having established a program plan means you can now produce the application basics by creating all the necessary widgets.

![](img/d06b1f1cf83677f6647237f0c7827141_267_0.png)

Toggle the value of a Button widget’s state property from NORMAL to DISABLED to steer the user – in this case the application must be reset before a further series of unique random numbers can be generated.

![](img/d06b1f1cf83677f6647237f0c7827141_267_1.png)

### lotto(widgets).py

- Launch a plain text editor, then begin a Python program by importing all features from the “tkinter” module

```python
# Widgets:
from tkinter import *
```

![](img/d06b1f1cf83677f6647237f0c7827141_267_2.png)

### lotto.gif

- Next, add statements to create a window object and an image object

```python
window = Tk()
img = PhotoImage( file = 'logo.gif' )
```

- Now, add statements to create all the necessary widgets

```python
imgLbl = Label( window, image = img )
label1 = Label( window, relief = 'groove', width = 2 )
label2 = Label( window, relief = 'groove', width = 2 )
label3 = Label( window, relief = 'groove', width = 2 )
label4 = Label( window, relief = 'groove', width = 2 )
label5 = Label( window, relief = 'groove', width = 2 )
label6 = Label( window, relief = 'groove', width = 2 )
getBtn = Button( window )
resBtn = Button( window )
```

- Then, add the widgets to the window using the grid layout manager – ready to receive arguments to specify how the widgets should be positioned at the design stage next

```python
# Geometry:
imgLbl.grid()
label1.grid()
label2.grid()
label3.grid()
label4.grid()
label5.grid()
label6.grid()
getBtn.grid()
resBtn.grid()
```

- Finally, add a loop statement to sustain the window

```python
# Sustain window:
window.mainloop()
```

- Save the file, then execute the program – to see the window appear containing all the necessary widgets

![](img/d06b1f1cf83677f6647237f0c7827141_268_0.png)

The **relief** property specifies a border style, and the **width** property specifies the label width in character numbers.

![](img/d06b1f1cf83677f6647237f0c7827141_269_0.png)

Having created all the necessary widgets here, you can now design the interface layout by adding arguments to specify how the widgets should be positioned. A horizontal design will position the logo Label on the left, and on its right all six other Labels in a row with both Buttons below this. The grid layout manager, which positions widgets in rows and columns, can easily produce this design by allowing the logo Label to span a row containing all six other Labels and also a row containing both Buttons. One Button can span four columns and the other Button can span two columns, arranged like this:

![](img/d06b1f1cf83677f6647237f0c7827141_270_0.png)

- 1. Edit the program started here – firstly by positioning the Label containing the logo in the first column of the first row, and have it span across the second row

```python
# Geometry:
imgLbl.grid(row=1, column=1, rowspan=2)
```

![](img/d06b1f1cf83677f6647237f0c7827141_270_1.png)

### lotto(layout).py

- 2. Next, position a Label in the second column of the first row, and add 10 pixels of padding to its left and right

```python
label1.grid(row=1, column=2, padx=10)
```

- 3. Now, position a Label in the third column of the first row, and add 10 pixels of padding to its left and right

```python
label2.grid(row=1, column=3, padx=10)
```

- 4. Position a Label in the fourth column of the first row, and add 10 pixels of padding to its left and right

```python
label3.grid(row=1, column=4, padx=10)
```

![](img/d06b1f1cf83677f6647237f0c7827141_271_0.png)

The grid layout manager's **rowspan** and **columnspan** properties work like the HTML **rowspan** and **colspan** table cell attributes.

- 5. Position a Label in the fifth column of the first row, and add 10 pixels of padding to its left and right

```python
label4.grid(row=1, column=5, padx=10)
```

- 6. Position a Label in the sixth column of the first row, and add 10 pixels of padding to its left and right

```python
label5.grid(row=1, column=6, padx=10)
```

- 7. Position a Label in the seventh column of the first row, then add 10 pixels of padding to the left side of the Label and 20 pixels of padding to the right side of the Label

```python
label6.grid(row=1, column=7, padx=(10, 20))
```

- 8. Next, position a Button in the second column of the second row, and have it span across four columns

```python
getBtn.grid(row=2, column=2, columnspan=4)
```

- 9. Now, position a Button in the sixth column of the second row, and have it span across two columns

```python
resBtn.grid(row=2, column=6, columnspan=2)
```

- 10. Save the file, then execute the program – to see the window appear containing all the necessary widgets now arranged in your grid layout design

![](img/d06b1f1cf83677f6647237f0c7827141_272_0.png)

The window size is automatically adjusted to suit the grid contents, and the Button widgets are automatically centered in the spanned column width.

![](img/d06b1f1cf83677f6647237f0c7827141_272_1.png)

Additional padding to the right of the Label in the final column of the first row extends the window width to simply create a small right-hand margin area.

![](img/d06b1f1cf83677f6647237f0c7827141_272_2.png)

The Buttons will expand to fit static text that will appear on each Button face – specified in the next stage.

## Assigning static properties

Having arranged all the necessary widgets in a grid layout [here](\_), you can now assign static values to the widgets. These values **will not** change during execution of the program.

- 1. Modify the program [here](\_) by inserting a new section just before the final loop statement, which begins with a statement specifying a window title

```python
# Static Properties:
window.title('Lotto Number Picker')
```

![](img/d06b1f1cf83677f6647237f0c7827141_273_0.png)

### lotto(static).py

- 2. Next, add a statement to prevent the user resizing the window along both the X axis and the Y axis – this will disable the window’s “resize” button

```python
window.resizeable(0, 0)
```

- 3. Now, add a statement to specify text to appear on the face of the first Button widget

```python
getBtn.configure(text='Get My Lucky Numbers')
```

- 4. Then, add a statement to specify text to appear on the face of the second Button widget

```python
resBtn.configure(text='Reset')
```

- 5. Save the file, then execute the program – to see the window now has a title, its resize button is disabled, and the buttons have now been resized to suit their text

![](img/d06b1f1cf83677f6647237f0c7827141_274_0.png)

![](img/d06b1f1cf83677f6647237f0c7827141_274_1.png)

The widget’s **configure()** method allows properties to be subsequently added or modified after they have been created.

## Initializing dynamic properties

Having specified values for static properties on the facing page, initial values can now be specified for those properties whose values will change dynamically during execution of the program.

- 1. Modify the program on the facing page by inserting another new section just before the final loop statement, which specifies that each small empty Label should initially display an ellipsis

```python
# Initial Properties:
label1.configure(text='...')
label2.configure(text='...')
label3.configure(text='...')
label4.configure(text='...')
label5.configure(text='...')
label6.configure(text='...')
```

- 2. Next, add a statement to specify that the second Button widget should initially be disabled

```python
resBtn.configure(state=DISABLED)
```

- 3. Save the file, then execute the program – to see each small Label now displays an ellipsis and that the “Reset” Button has been disabled

![](img/d06b1f1cf83677f6647237f0c7827141_275_0.png)
