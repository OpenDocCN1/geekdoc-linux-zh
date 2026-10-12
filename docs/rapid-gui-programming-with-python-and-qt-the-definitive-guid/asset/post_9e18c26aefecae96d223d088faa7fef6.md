
```python
    def rate(self):
        return self._rate

    def setRate(self, rate):
        if rate != self.__rate:
            self._rate = rate
            self.emit(SIGNAL("rateChanged"), self._rate)
```

Both the `rate()` and the `setRate()` methods can be connected to, since any Python callable can be used as a slot. If the rate is changed, we update the private `_rate` value and emit a custom `rateChanged` signal, giving the new rate as a parameter. We have also used the faster short-circuit syntax. If we wanted to use the standard syntax, the only difference would be that the signal would be written as `SIGNAL("rateChanged(float)")`. If we connect the `rateChanged` signal to the `setRate()` slot, because of the `if` statement, no infinite loop will occur. Let us look at the class in use. First we will declare a function to be called when the rate changes:

```python
def rateChanged(value):
    print "TaxRate changed to %.2f%%" % value
```

And now we will try it out:

```python
vat = TaxRate()
vat.connect(vat, SIGNAL("rateChanged"), rateChanged)
vat.setRate(17.5)     # No change will occur (new rate is the same)
vat.setRate(8.5)      # A change will occur (new rate is different)
```

This will cause just one line to be output to the console: “TaxRate changed to 8.50%”.

In earlier examples where we connected multiple signals to the same slot, we did not care who emitted the signal. But sometimes we want to connect two or more signals to the same slot, and have the slot behave differently depending on who called it. In this section’s last example we will address this issue.

![](img/9bfe0a027fcc8793bb087287001100dd_146_0.png)

**Figure 4.8 The Connections program**

The Connections program shown in Figure 4.8, has five buttons and a label. When one of the buttons is clicked the signals and slots mechanism is used to update the label’s text. Here is how the first button is created in the form’s `__init__()` method:

```python
button1 = QPushButton("One")
```

All the other buttons are created in the same way, differing only in their variable name and the text that is passed to them.

We will start with the simplest connection, which is used by `button1`. Here is the `__init__()` method's `connect()` call:

```python
self.connect(button1, SIGNAL("clicked()"), self.one)
```

We have used a dedicated method for this button:

```python
def one(self):
    self.label.setText("You clicked button 'One'")
```

Connecting a button's `clicked()` signal to a single method that responds appropriately is probably the most common connection scenario.

But what if most of the processing was the same, with just some parameterization depending on which particular button was pressed? In such cases, it is usually best to connect each button to the same slot. There are two approaches to doing this. One is to use partial function application to wrap a slot with a parameter so that when the slot is invoked it is parameterized with the button that called it. The other is to ask PyQt to tell us which button called the slot. We will show both approaches, starting with partial function application.

+ Partial function application 63

Back on page 65 we created a wrapper function which used Python 2.5's `functools.partial()` function or our own simple `partial()` function:

```python
import sys

if sys.version_info[:2] < (2, 5):
    def partial(func, arg):
        def callme():
            return func(arg)
        return callme
else:
    from functools import partial
```

Using `partial()` we can now wrap a slot and a button name together. So we might be tempted to do this:

```python
self.connect(button2, SIGNAL("clicked()"),
              partial(self.anyButton, "Two")) # WRONG for PyQt 4.0-4.2
```

Unfortunately, this won't work for PyQt versions prior to 4.3. The wrapper function is created in the `connect()` call, but as soon as the `connect()` call completes, the wrapper goes out of scope and is garbage-collected. From PyQt 4.3, wrappers made with `functools.partial()` are treated specially when they are used for connections like this. This means that the function connected to will not be garbage-collected, so the code shown earlier will work correctly.

+ PyQt 4.3

For PyQt 4.0, 4.1, and 4.2, we can still use partial(): We just need to keep a reference to the wrapper—we will not use the reference except for the connect() call, but the fact that it is an attribute of the form instance will ensure that the wrapper function will not go out of scope while the form exists, and will therefore work. So the connection is actually made like this:

```python
self.button2callback = partial(self.anyButton, "Two")
self.connect(button2, SIGNAL("clicked()"),
            self.button2callback)
```

When button2 is clicked, the anyButton() method will be called with a string parameter containing the text "Two". Here is what this method looks like:

```python
def anyButton(self, who):
    self.label.setText("You clicked button '%s'" % who)
```

We could have used this slot for all the buttons using the partial() function that we have just shown. And in fact, we could avoid using partial() at all and get the same results:

```python
self.button3callback = lambda who="Three": self.anyButton(who)
self.connect(button3, SIGNAL("clicked()"),
            self.button3callback)
```

+ Lambda call functions 61-3

Here we’ve created a lambda function that is parameterized by the button’s name. It works the same as the partial() technique, and calls the same anyButton() method, only with lambda being used to create the wrapper.

Both button2callback() and button3callback() call anyButton(); the only difference between them is that the first passes "Two" as its parameter and the second passes "Three".

+ PyQt 4.1.1

If we are using PyQt 4.1.1 or later, and we use lambda callbacks, we don’t have to keep a reference to them ourselves. This is because PyQt treats lambda specially when used to create wrappers in a connection. (This is the same special treatment that is expected to be extended to functools.partial() in PyQt 4.3.) For this reason we can use lambda directly in connect() calls. For example:

```python
self.connect(button3, SIGNAL("clicked()"),
            lambda who="Three": self.anyButton(who))
```

The wrapping technique works perfectly well, but there is an alternative approach that is slightly more involved, but which may be useful in some cases, particularly when we don’t want to wrap our calls. This other technique is used to respond to button4 and to button5. Here are their connections:

```python
self.connect(button4, SIGNAL("clicked()"), self.clicked)
self.connect(button5, SIGNAL("clicked()"), self.clicked)
```

Notice that we do not wrap the clicked() method that they are both connected to, so at first sight it looks like there is no way to tell which button called the clicked() method.* However, the implementation makes clear that we can distinguish if we want to:

```python
def clicked(self):
    button = self.sender()
    if button is None or not isinstance(button, QPushButton):
        return
    self.label.setText("You clicked button '%s'" % button.text())
```

Inside a slot we can always call sender() to discover which QObject the invoking signal came from. (This could be None if the slot was called using a normal method call.) Although we know that we have connected only buttons to this slot, we still take care to check. We have used isinstance(), but we could have used hasattr(button, "text") instead. If we had connected all the buttons to this slot, it would have worked correctly for all four.

Some programmers don't like using sender() because they feel that it isn't good object-oriented style, so they tend to use partial function application when needs like this arise.

There is actually one other technique that can be used to get the effect of wrapping a function and a parameter. It makes use of the QSignalMapper class, and an example of its use is shown in Chapter 9.

It is possible in some situations for a slot to be called as the result of a signal, and the processing performed in the slot, directly or indirectly, causes the signal that originally called the slot to be called again, leading to an infinite cycle. Such cycles are rare in practice. Two factors help reduce the possibility of cycles. First, some signals are emitted only when a real change takes place. For example, if the value of a QSpinBox is changed by the user, or programmatically by a setValue() call, it emits its valueChanged() signal only if the new value is different from the current value. Second, some signals are emitted only as the result of user actions. For example, QLineEdit emits its textEdited() signal only when the text is changed by the user, and not when it is changed in code by a setText() call.

If a signal-slot cycle does seem to have occurred, naturally, the first thing to check is that the code's logic is correct: Are we actually doing the processing we thought we were? If the logic is right, and we still have a cycle, we might be able to break the cycle by changing the signals that we connect to—for example, replacing signals that are emitted as a result of programmatic changes, with those that are emitted only as a result of user interaction. If the problem persists, we could stop signals being emitted at certain places in our code using QObject.blockSignals(), which is inherited by all QWidget classes and is

> It is conventional PyQt programming style to give a slot the same name as the signal that connects to it.

![](img/9bfe0a027fcc8793bb087287001100dd_149_0.png)
