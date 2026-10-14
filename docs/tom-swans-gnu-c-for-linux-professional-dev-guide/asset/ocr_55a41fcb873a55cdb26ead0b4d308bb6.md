# KEYBOARD INPUT

There are two main ways to intercept keyboard activity in V programs. You can receive keypress input at the window level, or you can do the same in the application object. The window gets first crack at incoming keypresses, so this is the usual method. Also, unless you need to program a global key that works the same regardless of which window is active, you probably want to process keypresses only for the window that has the input focus.

The next sample program, vKey, demonstrates how to intercept keypresses. For reference, the program displays two values—one that represents the key itself and another that indicates whether the Shift, Control, or Alt key is held down for keys that are not otherwise uniquely identified. Figure 30.3 shows a sample of the program’s window. The values in the window are for the M-F1 (Alt-F1) key on my keyboard.

Figure 30.3
The vkey application shows key and shift values for keypresses—in this case, M-F1 (Alt-F1).

![](bbox=[0.31, 0.51, 0.55, 0.66])

After color graphics, probably the second most hazardous programming job in X programming is dealing with keyboard input. (Programmers who deal with colormaps ought to receive combat pay.) Fortunately, V defines virtual key codes that should be the same regardless of the hardware. You might not have access to specialized keys in some cases, but you should have plenty of function, keypad, control, and alphanumeric keys for just about any application. Listing 30.9, cmdwin.cpp, shows the programming in vKey’s command window module that intercepts keypresses.

# LISTING 30.9 VKEY/CMDWIN.CPP (PARTIAL)

```
#include <v/v_defs.h>  // Need standard definitions

// Intercept keyboard events
void TCmdWindow::KeyIn(vKey keysym, unsigned int shift)
{
    myCanvas->SaveKeyValues(keysym, shift);  // Pass to canvas
    // Call ancestor function to handle unprocessed keystrokes
    vWindow::KeyIn(keysym, shift);
}
```

To get keypresses in a window object, override the KeyIn() function inherited from the vWindow class, usually through its descendant vCmdWindow. Add the following declaration to your window class’s public section and implement the function as shown in the listing:

virtual void KeyIn(vKey keysym, unsigned int shift);

The vKey value represents the key that was pressed. This might be an ASCII alphanumeric code, a control key value, or one of the symbols defined in V’s vkeys.h header file. These are