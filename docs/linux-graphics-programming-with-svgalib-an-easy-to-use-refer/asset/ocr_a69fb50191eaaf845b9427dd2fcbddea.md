# Table 15.3 Joystick shortcuts.

Full Function Shortcut
joystick_getbutton(i, 0) joystick_button1(i)
joystick_getbutton(i, 1) joystick_button2(i)
joystick_getbutton(i, 2) joystick_button3(i)
joystick_getbutton(i, 3) joystick_button4(i)
joystick_getbutton(0, 0) joystick_get1(i)
joystick_getbutton(0, 1) joystick_get2(i)
joystick_getbutton(0, 2) joystick_get3(i)
joystick_getbutton(0, 3) joystick_get4(i)
joystick_getaxis(i, 0) joystick_x(i)
joystick_getaxis(i, 1) joystick_y(i)
joystick_getaxis(i, 2) joystick_z(i)
joystick_getaxis(0, 0) joystick_getx(i)
joystick_getaxis(0, 1) joystick_gety(i)
joystick_getaxis(0, 2) joystick_getz(i)

Although it’s nice to have the flexibility that multiple input devices provide, I’ll admit that I still have a predilection for the keyboard.

# Summary Of Functions Introduced In This Chapter

Here is a summary of the functions covered in this chapter:

+   - void vga_setmousesupport(int stat)
+   - int mouse_init(char *dev, int type, int sampleire)
+   - void mouse_setxrange(int x1, int x2)
+   - void mouse_setyrange(int y1, int y2)
+   - void mouse_setwrap(int state)
+   - int vga_getmousetype(void)
+   - int mouse_update(void)
+   - void mouse_waitforupdate(void)
+   - void mouse_close(void)
+   - int mouse_getx(void)
+   - int mouse_gety(void)
+   - int mouse_getbutton(void)
+   - int mouse_getcaps(struct MouseCaps *caps)
+   - void vga_lockvc(void)