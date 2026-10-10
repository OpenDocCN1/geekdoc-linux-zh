Because programs must be written to take advantage of specific widget sets, programmers make the choice of which widget set to use. As a user or system administrator, you have no choice in the matter, except to use or not use particular programs. In some cases, if you want to use a particular program, you must install libraries that provide the widget set code. This task can be handled automatically by sysinstall or the FreeBSD ports system when you install the target program.

# Window Managers

X provides low-level window management routines, and widget sets provide tools that enable programmers to present useful information inside windows. Another component of practical X use is the window manager. A window manager adds functionality around windows. Most noticeably, window managers provide several components that immediately surround a window and enable a user to control its size and placement. Figure 13-1 shows a typical X window, with identified window manager components. These include

+   ■ **Title bar** The *title bar* or *drag bar* usually resides at the top of a window. It includes a name that identifies the window, and most window managers respond to click-and-drag operations in the title bar by moving the window around the screen.

![](bbox=[0.12, 0.49, 0.88, 0.88])

**Figure 13-1.** *A window manager creates border decorations around a window, enabling control of window position and size.*