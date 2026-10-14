
```cpp
#include "cmdwin.h"
#include <v_defs.h>    // Need standard definitions
#include <v/keys.h>    // Need virtual key symbols

// Define menu item constants not in v_defs.h
const ItemVal m_Width  = 100;
const ItemVal m_Width1 = 101;
const ItemVal m_Width2 = 102;
const ItemVal m_Width3 = 103;
const ItemVal m_Width4 = 104;
const ItemVal m_Width5 = 105;
const ItemVal m_Width6 = 106;
const ItemVal m_Width7 = 107;
const ItemVal m_Width8 = 108;
const ItemVal m_Width9 = 109;

// Define the File menu's commands
static vMenuItem M_File[] =
{
  {"New", M_New, isSens, notChk, noKeyLbl, noKey, noSub},
  {"", M_Line, notSens, notChk, noKeyLbl, noKey, noSub},
  {"Exit", M_Exit, isSens, notChk, "Alt-X", 'x', noSub},
  VKM_Alt},
  {NULL}
};

static vMenu WidthMenu[] =
{
  {"1", m_Width1, isSens, isChk, "F1", VK_F1, noSub},
  {"2", m_Width2, isSens, notChk, "F2", VK_F2, noSub},
  {"3", m_Width3, isSens, notChk, "F3", VK_F3, noSub},
  {"4", m_Width4, isSens, notChk, "F4", VK_F4, noSub},
  {"5", m_Width5, isSens, notChk, "F5", VK_F5, noSub},
  {"6", m_Width6, isSens, notChk, "F6", VK_F6, noSub},
  {"7", m_Width7, isSens, notChk, "F7", VK_F7, noSub},
  {"8", m_Width8, isSens, notChk, "F8", VK_F8, noSub},
  {"9", m_Width9, isSens, notChk, "F9", VK_F9, noSub},
  {NULL}
};

// Define the top-level menu bar
vMenu MenuBar[] =
{
  {&File, M_File, isSens, notUsed, notUsed, noKey,
   &FileMenu[0]},
  {&Width, m_Width, isSens, notUsed, notUsed, noKey,
   &WidthMenu[0]},
  {NULL}
};

// Our command window constructor
TCmdWindow::TCmdWindow(char* name, int width, int height) :
```

## LISTING 30.12 CONTINUED

```
vCmdWindow(name, width, height)  // Call ancestor constructor
{
    widthMenuItem = m_Width1;          // Remember checked menu
    myMenu = new vMenuPane(MenuBar);   // Create menu pane
    AddPane(myMenu);                   // Add it to our window
    myCanvas = new TCanvasPane;        // Create our canvas object
    AddPane(myCanvas);                 // Add it to our window
    pen.SetColor(0, 0, 0);             // Set pen color to black
    pen.SetWidth(1);                   // Set initial pen width
    myCanvas->SetPen(pen);             // Set pen into canvas
    ShowWindow();                      // Make window visible
}

// Our command window destructor
TCmdWindow::~TCmdWindow()
{
    delete myMenu;   // One for each "new" in constructor
    delete myCanvas;
}

// Respond to menu selections and other commands
void TCmdWindow::WindowCommand(
    ItemVal id, ItemVal val, CmdType cType)
{
    switch (id) {
        case M_New:
            myCanvas->Clear(); // Erase window's canvas
            break;
        case m_Width1:                 // Fall-through cases for Window menu
        case m_Width2:
        case m_Width3:
        case m_Width4:
        case m_Width5:
        case m_Width6:
        case m_Width7:
        case m_Width8:
        case m_Width9:
            pen.SetWidth(id - m_Width1 + 1);   // Change pen width
            myCanvas->SetPen(pen);             // Insert in canvas
            SetValue(widthMenuItem, 0, Checked); // Uncheck old cmd
            widthMenuItem = id;
            SetValue(widthMenuItem, 1, Checked); // Check new cmd
            break;
        case M_Exit:                   // User selected File|Exit command
            theApp->Exit();                // Exit the application
            break;
        default:                       // Route unhandled commands
            vCmdWindow::WindowCommand(id, val, cType);
            break;
    }
}
```

For most menus, include the V headers v_defs.h and vkeys.h. The first header makes standard menu command values such as M_Exit available. The second header includes virtual key codes used in defining accelerator keys.

For consistency among applications, you are urged to use V’s standard symbols when possible. However, you are free to invent your own. In this case, I defined new symbols for the program’s Width menu as follows:

```
const ItemVal m_Width = 100;
const ItemVal m_Width1 = 101;
...
const ItemVal m_Width9 = 109;
```

The first value represents the menu item; the others identify each command in the menu. You may use any names, but they should be of type ItemValue and to lessen confusion are best prefixed with lowercase m_. By convention, start your own symbols at 100 and increase by one.

> Standard values are reserved from 30,000 and up. Assign values less than 30,000 to all your own symbolic menu and other component constants. (In the program’s source code, however, don’t insert a comma in numbers such as 30,000.)

The next step is to create a static struct object for each of your program’s pull-down menus. These structs represent the commands in each menu, not the top-level menu name such as File or Width in the sample program. For example, the program defines its File menu commands with the following struct array:

```
static vMenu FileMenu[] =
{
  {"New", M_New, isSens, notChk, noKeyLbl, noKey, noSub},
  {"-", M_Line, notSens, notChk, noKeyLbl, noKey, noSub},
  {"Exit", M_Exit, isSens, notChk, "Alt-X", 'x', noSub, VKM_Alt},
  {NULL}
};
```

Each item in the vMenu struct array may consist of seven or eight items. The list must end with {NULL}. First is a string to display in the menu. Next is the item’s symbolic identifier—either a standard one such as M_New, or one of your own. The isSens value indicates whether this item is user-selectable at runtime or is disabled by default. To create a separator line, assign a single dash string as its name and use the M_Line symbol along with notSens as shown (you don’t want users selecting a separator line). The notChk label indicates no check mark next to this item. The noKeyLbl indicates no additional accelerator key label. Notice that the Exit command specifies Alt-X as this value—it’s shown in brackets in the window (at least in my window manager). To indicate the accelerator key value, use noKey if there is none, or an ASCII character constant such as 'x' here. The noSub label indicates there is no submenu—you can use the name of another vMenu struct here to create a submenu, opened by selecting this command. Finally, specify an optional shift key such as VKM_Alt. This is
