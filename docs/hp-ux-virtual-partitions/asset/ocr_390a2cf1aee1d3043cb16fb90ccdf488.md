icon. A blank is useful as a space holder. An icon can start an action or application or be a drop zone.

+   - **ICON** - The bitmap to display on the front panel. Front-panel bitmaps are located in the `/usr/dt/appconfig/icons` directory.
+   - **CONTAINER_NAME** - The name of the container that holds the control. This must correspond to the name of an actual container listed in `dtwm.fp`.
+   - **CONTAINER_TYPE** - The type of container that holds the control. This can be **BOX**, **SWITCH**, or **SUBPANEL**, but it must agree with the type of the container name.
+   - **PUSH_ACTION** - This is what happens when the control button is pushed. **PUSH_ACTION** is just one of several possible actions. For more information, see the `dtwm` man page.

To remove a control button from the front panel, type a pound sign (#) in the left-most column of the **CONTROL** definition line. The (#) turns the control specification into a comment line.

Add a control button by editing the `dtwm.fp` file:

+   1. Copy `dtwm.fp` from `/usr/dt/appconfig/types/C` to `/etc/dt/appconfig/types/C`.
+   2. Add the new control definition using the following format:

```
CONTROL  NewControl
{
TYPE            icon
CONTAINER_NAME Top
CONTAINER_TYPE  BOX
ICON        NewControlBitmap
PUSH_ACTION NewControlExecutable
}
```

Action and File Types have their own peculiarities in that each has a couple of parts, and each must live in its own directory location. These peculiarities will become clear as we create an action on the subpanel. The following are the recommended locations in which to create an action or file type definition: