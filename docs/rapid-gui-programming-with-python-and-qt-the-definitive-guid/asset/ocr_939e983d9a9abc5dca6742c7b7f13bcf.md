We also learned that we do not have to formally declare our own custom signals: We can simply emit them using QObject.emit(), along with any additional parameters we want to pass.

# ## Exercise

Write a dialog-style application that calculates compound interest. The application should be very similar in style and structure to the Currency application, and should look like this:

![](bbox=[0.38, 0.29, 0.62, 0.41])

The amount should be automatically recalculated every time the user changes one of the variable factors, that is, the *principle, rate, or years*. The years combobox should have the texts “*1 year*”, “*2 years*”, “*3 years*”, and so on, so the number of years will be the combobox’s current index + 1. The compound interest formula in Python is `amount = principal * ((1 + (rate / 100.0)) ** years)`. The `QDoubleSpinBox` class has `setPrefix()` and `setSuffix()` methods which can be used for the “$” and “%” symbols. The whole application can be written in around 60 lines.

Hint: The updating can be done by connecting suitable spinbox and combobox signals to an `updateUi()` slot where the calculations are performed and the amount label is updated.

A model answer is provided in the file `chap04/interest.pyy`.