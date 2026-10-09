```
if(blender_w) return 1;

XQueryTree(dpy, w, &root_return, &parent_return, &children, &nchildren);
if(children==NULL) {
return 0;
} else {
int i;
for(i=0; i<nchildren && !blender_w; i++) {
char *wm;
XFetchName(dpy, children[i], &wm);
if(wm && strcmp(wm, "Blender")==0) {
blender_w = children[i];
} else {
recursive_find_blender_window(children[i]);
}
Xfree(wm);
}
Xfree(children);
}

void blender_xcontroller::find_blender_window(void)
{
blender_w = 0;
recursive_find_blender_window(DefaultRootWindow(dpy));
}

void blender_xcontroller::press_key(int code)
{
XEvent event;
unsigned long mask;

event.type = KeyPress;
event.xkey.type = KeyPress;
event.xkey.serial = 30;
event.xkey.send_event = FALSE;
event.xkey.display = dpy;
event.xkey.window = blender_w;
event.xkey.root = DefaultRootWindow(dpy);
event.xkey.subwindow = 0;
event.xkey.time = 1954543190;
event.xkey.x = event.xkey.y = 0;
event.xkey.x_root = event.xkey.y_root = 0;
event.xkey.state = 0;
event.xkey.keycode = code;
event.xkey.same_screen= TRUE;
mask = 1;
XSendEvent(dpy, blender_w,
TRUE, mask, &event);

Xflush(dpy);
}

void blender_xcontroller::release_key(int code)
{
XEvent event;
unsigned long mask;

event.type = KeyRelease;
```