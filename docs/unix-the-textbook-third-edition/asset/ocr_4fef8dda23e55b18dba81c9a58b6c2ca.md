```
/* the window was exposed redraw it! */
    redraw();
}
if (event.type==KeyPress&&
    XLookupString(&event.xkey,text,255,&key,0)==1) {
/* use the XLookupString routine to convert the invent
KeyPress data into regular text.
*/
    if (text[0]=='q') {
        close_x();
    }
    printf("You pressed the %c key\n",text[0]);
}
if (event.type==ButtonPress) {
/* report where the mouse Button was Pressed */
    int x=event.xbutton.x;
    y=event.xbutton.y;
    strcpy(text,"UNIX Rocks");
    XSetForeground(dis,gc,rand()%event.xbutton.x%255);
    XDrawString(dis,win,gc,x,y, text, strlen(text));
}
}
void init_x() {
/* Set the colors black and white */
    unsigned long black,white;

    dis=XOpenDisplay((char *)0);
    screen=DefaultScreen(dis);
    black=BlackPixel(dis,screen),
    white=WhitePixel(dis, screen);
    win=XCreateSimpleWindow(dis,DefaultRootWindow(dis),0,0,
        300, 300, 5,black, white);
    XSetStandardProperties(dis,win,"Report","E",None,NULL,0,NULL);
    XSelectInput(dis, win, ExposureMask|ButtonPressMask|KeyPress
Mask);
    gc=XCreateGC(dis, win, 0,0);
    XSetBackground(dis,gc,white);
    XSetForeground(dis,gc,black);
    XClearWindow(dis, win);
    XMapRaised(dis, win);
};

void close_x() {
/* Cleanup */
XFreeGC(dis, gc);
XDestroyWindow(dis,win);
```