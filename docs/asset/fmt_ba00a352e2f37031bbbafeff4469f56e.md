
```cpp
/*
 * ex26-01KDE.h
 */

#include <kapp.h>
#include <ktmainwindow.h>
#include <qpushbutton.h>
#include <qmenubar.h>
#include <qpopupmenu.h>

class KDEHelloWorld : public KMainWindow
{
public:
  KDEHelloWorld();
  void closeEvent(QCloseEvent *);
public slots:
  void SlotGreet();
  void SlotQuit();
  void SlotBrowse();
private:
  QPushButton *m_btnGreet;
  QPushButton *m_btnQuit;
  QPushButton *m_btnBrowse;
  QMenuBar *m_Menu;
  QPopupMenu *m_MenuApp;
};
```

```cpp
/*
 * ex26-01KDE.cxx
 */

#include "ex26-01.h"
#include <kapp.h>
#include <ktmainwindow.h>
#include <kmsbox.h>

KDEHelloWorld::KDEHelloWorld() : KMainWindow()
{
  m_btnGreet = new QPushButton("Greet", this);
  m_btnGreet->setGeometry(45,30,50,20);
  m_btnGreet->show();
  connect(m_btnGreet, SIGNAL(clicked()), SLOT(SlotGreet()));

  m_btnQuit = new QPushButton("Exit", this);
  m_btnQuit->setGeometry(105,30,50,20);
  m_btnQuit->show();
  connect(m_btnQuit, SIGNAL(clicked()), SLOT(SlotQuit()));

  m_btnBrowse = new QPushButton("Browse", this);
  m_btnBrowse->setGeometry(155,30,50,20);
  m_btnBrowse->show();
  connect(m_btnBrowse, SIGNAL(clicked()), SLOT(SlotBrowse()));

  m_MenuApp = new PopupMenu();
  m_MenuApp->insertItem("&Greet", this, SLOT(SlotGreet()));
  m_MenuApp->insertItem("&Quit", this, SLOT(SlotQuit()));
  m_MenuApp->insertItem("&Browse", this, SLOT(SlotBrowse()));
  m_Menu = new KMenuBar(this);
  m_Menu->insertItem("&Application", m_MenuApp);
}
```

```cpp
void KDEHelloWorld::closeEvent(QCloseEvent *)
{
  qApp::quit();
}
```

```cpp
void KDEHelloWorld::SlotGreet()
{
  KMessageBox(0, "Hello World!");
}
```

```cpp
void KDEHelloWorld::SlotBrowse()
{
  QString fileName = QFileDialog::getOpenFileName(QString(), QString(), this);
}
```

```cpp
void KDEHelloWorld::SlotQuit()
{
  close();
}
```

```cpp
int main(int argc, char **argv)
{
  KApplication MyApp(argc, argv);
  KMainWindow *MyWindow = new KMainWindow();
  MyWindow->setGeometry(50,50,200,100);

  MyApp.setWidget(MyWindow);
  MyWindow->show();
  return 0;
}
```

```cpp
// 使用以下命令编译文件：
moc ex26KDE.h -o ex26KDE.moc
g++ -c -IKDE/include -IQTDIR -fno-rtti ex26KDE.cxx
g++ -LKDE/lib -lkdecore -lkui -lqt -o ex26KDE.o
```

## 练习和测验答案

在 `ex26-02wxWin.cpp` 中，我们在 `MyFrame` 声明中添加了一个额外的按钮变量 `m_btnBrowse`。我们在 `MyFrame::OnInit()` 构造函数中初始化该成员并创建按钮，并在 `EVENT_TABLE()` 声明中将事件 `ID_Browse` 连接到处理器 `MyFrame::OnBrowse()`。点击按钮时，处理器调用 `wxFileSelector()` 来显示标准的文件浏览对话框。

```cpp
/*
 * ex26-02wxWin.cpp
 */

#ifdef __WX__
// #pragma implementation
#endif

// 支持预编译的编译器包含了 wx/wx.h。
#include "wx/wxprec.h"

#ifdef _BORLANDC
// #pragma header
#endif

#ifndef WX_PRECOMP
#include "wx/wx.h"
#endif

class MyApp: public wxApp
{
    virtual bool OnInit();
}

class MyFrame: public wxFrame
{
public:
    MyFrame(const wxString& title, const wxPoint& pos,
    const wxSize& size);
    void OnQuit(wxCommandEvent& event);
    void OnGreet(wxCommandEvent& event);
    void OnBrowse(wxCommandEvent& event);
    DECLARE_EVENT_TABLE()
private:
    wxPanel *m_panel;
    wxButton *m_btnGreet;
    wxButton *m_btnQuit;
    wxButton *m_btnBrowse;
};
```

![](img/a66ce94ee9cc26c70f560bcd3600c_1084_0.png)

```cpp
enum {
    ID_Quit = 1,
    ID_Greet,
    ID_Browse,
}
```

```cpp
BEGIN_EVENT_TABLE(MyFrame, wxFrame)
EVT_MENU(ID_Quit, MyFrame::OnQuit)
EVT_MENU(ID_Greet, MyFrame::OnGreet)
EVT_BUTTON(ID_Greet, MyFrame::OnGreet)
EVT_BUTTON(ID_Quit, MyFrame::OnQuit)
EVT_BUTTON(ID_Browse, MyFrame::OnBrowse)
END_EVENT_TABLE()
```

```cpp
IMPLEMENT_APP(MyApp)
bool MyApp::OnInit() {
    MyFrame *frame = new MyFrame("Hello World",
    wxPoint(50,50), wxSize(200,100));
    frame->Show(TRUE);
    SetTopWindow(frame);
    return TRUE;
}
```

```cpp
MyFrame::MyFrame(const wxString& title,
const wxPoint& pos, const wxSize& size)
: wxFrame(wxFrame *)NULL, -1, title, pos, size) {

wxSize panelSize = GetClientSize();
const int buttonWidth=50;
const int buttonHeight=25;
const int buttonSpacing=10;
const wxSize buttonSize(buttonWidth, buttonHeight);
```

```cpp
int height = panelSize.GetHeight();
int width = panelSize.GetWidth();
m_panel = new wxPanel(this, -1, wxPoint(0, 0), panelSize);

m_btnGreet = new wxButton(m_panel, ID_Greet,
T("Greet..."),
wxPoint(width/2-(buttonWidth+buttonSpacing), 10), buttonSize);
m_btnQuit = new wxButton(m_panel, ID_Quit,
T("Quit"),
wxPoint(width/2)-(buttonWidth/2), 10), buttonSize);

m_btnBrowse = new wxButton(m_panel, ID_Browse,
T("Browse..."),
wxPoint(width/2)+(buttonWidth/2+buttonSpacing), 10), buttonSize);

wxMenu *menuApp = new wxMenu;

menuApp->Append(ID_Greet, &"Greet...");
menuApp->Append(ID_Browse, &"Browse...");
menuApp->AppendSeparator();
menuApp->Append(ID_Quit, &"Quit");

wxMenuBar *menuBar = new wxMenuBar;
menuBar->Append(menuApp, "Application");

SetMenuBar(menuBar);
```

```cpp
void MyFrame::OnQuit(wxCommandEvent& event)
{
    Close(TRUE);
}
```

```cpp
void MyFrame::OnBrowse(wxCommandEvent& event)
{
    const wxString& file = ::wxFileSelector("Select a file");
}
```

```cpp
void MyFrame::OnGreet(wxCommandEvent& event)
{
    wxMessageBox("This is a wxWindows Hello world sample,\nGreet: Hello World", wxOK | wxICON_INFORMATION, this);
}
```

```cpp
// 使用以下命令编译文件：
// gcc -Wall `gnome-config --cflags gnome gnomeui \
// `LDFLAGS=gnome-config \
// -libs gnome gnomeui` ex26-02wxWin.c -o ex26-02wxWin
```

### 3. 扩展练习 2 中的代码，以便当你点击 OK 并选择文件时，程序将将其显示在主窗口的文本控件中。

我们进一步扩展了 `ex26-0KDE.h` 中的 `KDEHelloWorld` 类声明，包含一个 `QString` 成员变量用于存储我们所选择的文件名，以及一个在客户端区域显示文本的 `QTextView` 控件。我们在构造函数中创建了文本视图，并将其任意放置在主窗口上。

然后，我们扩展了 `SlotBrowse()` 函数，以从文件浏览器对话框获取文件名，然后使用 `QFile` 对象对其进行初始化。我们通过 `QFile` 的 `open()` 成员打开文件，循环读取每一行，直到将整个文件读取到一个临时字符串中。然后，我们将该字符串设置为要在文本视图中显示的文本。这是一种非常简单的方法，且仅处理文本文件：如果你读取的是二进制文件，可能会看到一些异常结果。

```cpp
/*
* ex26-03KDE.h
*/
#include <kapp.h>
#include <ktmainwindow.h>
#include <qpushbutton.h>
#include <menubar.h>
#include <qpopupmenu.h>

class KDEHelloWorld : public KMainWindow {
    Q_OBJECT
public:
    KDEHelloWorld(QCloseEvent);
    void closeEvent(QCloseEvent);
public slots:
    void SlotGreet();
    void SlotQuit();
    void SlotBrowse();
private:
    QPushButton *m_btnGreet;
    QPushButton *m_btnQuit;
    QPushButton *m_btnBrowse;
    QTextView *m_textView;
    QString *m_FileName;

    KMenuBar *m_Menu;
    QPopupMenu *m_MenuApp;
};
/*
* ex26-03KDE.cxx
*/
#include "ex26-03KDE.03.moc"
#include <kapp.h>
#include <ktmainwindow.h>
```

## 练习与测验答案
