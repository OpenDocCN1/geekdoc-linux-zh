**return_fd** version returns the file descriptor of the mouse device to allow you to do further tricks with the mouse (but the *filehandle* may change during a VC switch). The other version just returns 0 if successful. Note that both versions return -1 on error.

```
```cpp
void mouse_close(void)
```
```

Closes the mouse device file. This should be called at the end of the program (if a mouse is used), because it tries to restore the original mouse state, if the state has been changed.

```
```cpp
int mouse_update(void)
```
```

This reads in mouse events from the mouse buffer and updates the internal SVGAlib variables that store the current mouse position and button states. If there are no events to be read, this routine returns immediately. The function returns 0 if there was no event and a nonzero value otherwise.

```
```cpp
void mouse_waitforupdate(void)
```
```

This reads in mouse events from the mouse buffer and updates the internal SVGAlib variables that store the current mouse position and button states. If there are no events, the function does not return until one occurs.

```
```cpp
void mouse_setscale(int s)
```
```

This routine sets the scale factor between the motion reported by the mouse and the size of one pixel. The larger the *scale*, the slower the mouse cursor appears to move. The *scale* may be set to any nonzero integer. Negative *scales* result in flipped axes. Currently, there is no support for scale factors between 0 and 1, which would make the mouse appear faster than usual. If this routine is never called, *scale s* defaults to 1.

```
```cpp
void mouse_setwrap(int state)
```
```

This routine determines what to do if the mouse position reaches a boundary. *state* should be either *MOUSE_WRAP MOUSE_NOWRAP* or a bitwise OR of *MOUSE_WRAPX MOUSE_WRAPY MOUSE_WRAPXZ* . These define if all or the respective coordinates wrap or are clipped at the ends. This variable has been overloaded for the case of multidimensional mice that support rotations and can be used to select the coordinate system used to return the current position of the mouse.

If the value of *state* is also ordered with *MOUSE_ROT_RX RY RZ*, rotational information will be returned as the angular position, as expressed by the total angle wound around the *x*, *y*, and *z* axes. This is the simplest coordinate system to use, but it's also the least useful, because angular rotations about perpendicular axes don't commute. There are situations where this system might be useful for controlling truly independent quantities, such as color, with each axis being used to dial a level of red, green, or blue, but for modeling the actual orientation of a physical object, it's utterly hopeless.