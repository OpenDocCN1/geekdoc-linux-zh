# LISTING 29.4 MYCMDWD.CPP (PARTIAL)

```
#include <v/notice.h>  // for vNoticeDialog
#include <v/keys.h>  // to map keys
#include "mycmdw.h"  // our header

void myTimer::TimerTick()
{
    // update clock
    cmdw->WindowCommand(lblCurTime, lblCurTime, C_Button);
}

myCmdWindow::myCmdWindow(char* name, int width, int height) :
    vCmdWindow(name, width, height)
{
    // The Menu Bar
    myMenu = new vMenuPane(StandardMenu);
    AddPane(myMenu);
    // The Command Pane
    myCmdPane = new vCommandPane(ToolBar);
    AddPane(myCmdPane);
    // The Canvas
    myCanvas = new myCanvasPane;
    AddPane(myCanvas);
    // The Status Bar
    myStatus = new vStatusPane(StatBar);
    AddPane(myStatus);
    _timer = new myTimer(this);  // create timer
    _timer->TimerSet(1000);      // 1 second intervals
    // Associated dialogs
    myDlg = new myDlg(this,name);
    myMDlg = new myModalDialog(this,name);
    // Show Window
    ShowWindow();
    WindowCommand(lblCurTime,lblCurTime,C_Button);// update clock
    myCanvas->ShowVScroll(1);  // Show Vert Scroll
    myCanvas->ShowHScroll(1);  // Show Horiz Scroll
}

myCmdWindow::~myCmdWindow()
{
    delete myMenu;
    delete myCanvas;
    delete myCmdPane;
    delete myStatus;
    _timer->TimerStop();  // end it
    delete _timer;  // free it
    delete myDlg;
    delete myMDlg;
}

void myCmdWindow::KeyIn(vKey keysym, unsigned int shift)
{
    vCmdWindow::KeyIn(keysym, shift);
}

void myCmdWindow::WindowCommand(ItemVal id,
```