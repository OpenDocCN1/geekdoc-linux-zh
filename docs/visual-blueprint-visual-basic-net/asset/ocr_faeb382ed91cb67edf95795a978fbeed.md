# Extra

You must develop your application carefully for the Timer control to function properly. The Timer control does not operate in a separate thread, meaning it can only function if your application is idle. If your application is running a calculation or intensive loop of operations and you want the Timer control to function at the same time, you must call the DoEvents method of the Application object. This method allows other queued events and operations to occur like the Timer control's Tick event and UI redraws. Keep in mind that when you call DoEvents, events such as mouse clicks fire, so you must make sure that the user does not attempt to start an action that is already in process again.

# Example:

```
Do
' do lots of processing
' ...
' let the application do any necessary queued actions
Application.DoEvents()
Loop Until done
```

![](bbox=[0.07, 0.51, 0.48, 0.79])

![](bbox=[0.52, 0.51, 0.94, 0.79])

The Code Editor loads the Tick event.

8 Type code to run when the control raises the Tick event.

In the example, the code increments a label on the form.

9 Press F5 to run the project.

The Timer raises the event as specified in the Interval property.