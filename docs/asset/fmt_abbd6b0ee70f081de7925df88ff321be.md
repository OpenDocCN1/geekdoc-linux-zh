
```cpp
#include <iostream>
#include "lst25-02.h"

Pipe::Pipe() {
    init_(false),
    read_(false)
}

Pipe::~Pipe() {
    if (init_)
        Destroy();
}

int Pipe::Create() {
    if (pipe(pipe_) >= 0)
        init_ = true;
}

int Pipe::Destroy() {
    if (read_)
        close(pipe_[0]);
    else
        close(pipe_[1]);
}

void Pipe::SetToRead() {
    read_ = true;
    close(pipe_[1]);
}

void Pipe::SetToWrite() {
    read_ = false;
    close(pipe_[0]);
}

int Pipe::ReadFromPipe(char* buf) {
    if (read_)
        return -1;

    read(pipe_[0], buf, strlen(buf));
}
```

```cpp
int Pipe::WriteToPipe(char* buf) {
    if (read_)
        return -1;

    write(pipe_[1], buf, strlen(buf));
}
```

### 3. 扩展 `NamedPipe` 类以打开非阻塞管道，并创建读写例程以反映没有可用数据。这样做使得 `NamedPipe` 对象可以检测到没有数据，从而执行其他操作。

第一个列表是 `ex25-08.cxx`——客户端；第二个列表是 `ex25-09.cxx`——服务器；第三个列表是 `ex25-10.cxx`——命名管道实现；第四个列表是 `ex25-11.h`——文件 `np.h`；最后一个列表是 `ex25-12.mak`——makefile。你需要重命名文件，以便 `make` 命令和 `#include` 指令正常工作。

```cpp
#include <iostream>
#include "np.h"
```

```cpp
int main(int argc, char** argv) {
    NamedPipe* pipe = new NamedPipe;

    pipe->Create();
    pipe->Open();

    int i = 0;
    do {
        const int len = 32;
        char buf[len];

        sprintf(buf, "%d", i++);

        pipe->Write(&buf[0], static_cast<int>(strlen(buf)));

        cout << "client" << buf << endl;
    } while (i < 10);

    pipe->Close();

    pipe->Destroy();

    delete pipe;
}
```

```cpp
#include <iostream>
#include "np.h"

int main(int argc, char** argv) {
    NamedPipe* pipe = new NamedPipe;

    pipe->Create();
    pipe->Open();

    int i = 0;
    do {
        const int len = 32;

        char buf[len];

        if (pipe->Read(buf, len) > 0)
            cout << "server" << buf << endl;
    } while (i < 10);

    pipe->Close();
    pipe->Destroy();

    delete pipe;
}
```

```cpp
#include <stdio.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h>
#include <sys/stat.h>
#include <fcntl.h>
#include "np.h"

NamedPipe::NamedPipe() :
    init_(false),
    fp_(static_cast<int>(0)),
    name_(static_cast<char*>(0))
{
}

NamedPipe::~NamedPipe() {
    if (init_)
        Destroy();
}

int NamedPipe::Create() {
    char name[] = "NP";
    if (mkfifo(name, S_IFIFO | 0666) == 0) {
        name_ = new char[strlen(name)];
        strcpy(name_, name);
        init_ = true;
    }
    return init_;
}

int NamedPipe::Open() {
    // 非阻塞 IO 使用 O_NONBLOCK 标志
    fp_ = open(name_, O_RDWR | O_NONBLOCK);
    return fp_;
}

int NamedPipe::Close() {
    if (fp_ != 0)
        close(fp_);
    fp_ = static_cast<int>(0);
}

int NamedPipe::Destroy() {
    Close();
    delete[] name_;
    init_ = false;
}

int NamedPipe::Read(char* buf, int len) {
    if (fp_ == 0)
        return -1;

    int n = read(fp_, buf, len);
    if (n <= 0)
        return -1;
    return n;
}

int NamedPipe::Write(char* buf, int len) {
    if (fp_ == 0)
        return -1;

    int n = write(fp_, buf, len);
    if (n <= 0)
        return -1;
    return n;
}
```

```cpp
#include <sys/types.h>
#include <sys/stat.h>
#include <stdio.h>
#include <lst25-02.h>

class NamedPipe {
public:
    NamedPipe();
    ~NamedPipe();

    int Create();
    int Create(char* name);
    int Open();
    int Close();

    int Read(char* buf, int len);
    int Write(char* buf, int len);

private:
    NamedPipe& operator=(const NamedPipe&); // 禁止拷贝

    bool init_;
    int fp_;
    char* name_;
};
#endif
```

```makefile
INCLUDES=-I../ -I../Key
CFLAGS=-c
OBJS=../obj/key.o ../obj/np.o
all: client server

np.o : np.cxx np.h
	gcc $(CFLAGS) -o np np.cxx $(INCLUDES)
	cp np.o ../obj

client.o : client.cxx
	gcc $(CFLAGS) -o client.o client.cxx $(INCLUDES)

server.o : server.cxx
	gcc $(CFLAGS) -o server.o server.cxx $(INCLUDES)

client: client.o
	gcc -o client $(OBJS) -lstdc++

server: server.o
	gcc -o server $(OBJS) -lstdc++
```

# 第 26 天

## 测验

- **1. 事件驱动程序和过程程序的区别是什么？**

  过程程序从开始开始根据输入遵循控制路径直到结束。事件驱动程序在循环中等待外部事件发生，然后对这些事件做出响应。

- **2. 在计算术语中，什么是控件（widget）？**

  在计算术语中，控件是图形用户界面（GUI）的元素，用于显示信息或为用户与操作系统及应用程序的交互提供特定方式。

- **3. 什么是回调函数（callback function），为什么它们容易出错？**

  回调函数是通过引用传递给另一个函数。回调函数通常定义为类型 `(void) (*func)`，这意味着编译器在编译时无法知道传递的函数是否类型合适。即使类型声明是安全的，不负责任的程序员提供的指针可能是 `NULL` 或无效，这通常会导致可怕的核心转储（core dump）。

- **4. 什么是 Qt 槽（slot），它是如何响应信号的？**

  槽是一个普通的成员函数，你使用 `connect()` 函数将其链接到信号。以这种方式连接到信号的槽会在指定对象发射连接信号时被调用。

## 附录 D

- **5. 信号和槽是类型安全的。这意味着什么？为什么这是一件好事？**

  槽和信号总是类型正确的，这意味着槽永远不会接收错误类型的信号，你也不会从那里产生核心转储。事实上，槽和信号是松耦合的，因为发射信号的对象不知道其信号是否被槽捕获或被完全忽略。

- **6. 你如何将以下 wxWindows 事件处理程序绑定到 ID 为 `ID_MY_HELP` 的菜单项的 `EVT_MENU` 事件？假设 `OnHelp()` 是 `MyFrame` 类的成员，且 `MyFrame` 派自 `wxFrame`。**

  ```cpp
  void OnHelp(wxCommandEvent& WXUSED(event));
  使用此事件表声明：
  BEGIN_EVENT_TABLE(MyFrame, wxFrame)
  EVT_MENU(ID_MY_HELP, MyFrame::OnHelp)
  END_EVENT_TABLE()
  ```

- **7. `IMPLEMENT_APP()` 宏做什么？**

  `IMPLEMENT_APP()` 宏展开 wxWindows 的 `main()` 函数，并向程序员隐藏主事件循环的细节。

- **8. `Q_OBJECT` 宏做什么？**

  `Q_OBJECT` 宏由元对象编译器（MOC）使用，用于将类声明中 Qt 特有的信号和槽部分转换为标准 C++ 编译器可以理解的形式。

## 练习

### 1. 以 `buttons.cc` 源文件为基础，扩展程序，使得在点击按钮时 `callback` 类弹出一个对话框，而不是直接写入标准输出（stdout）。

在这里我们将看到创建了一个新的静态成员函数 `callback::do_message()` 作为回调函数。在其中，我们通过调用 `gnome_message_box_new()` 创建一个对话框，并通过 `gnome_dialog_run()` 显示它。然后我们在通过 `gtk_signal_connect()` 连接的回调函数中调用 `do_message()`。

```cpp
/* 基础 gnome 包含 */
#include <gnome.h>

class callback {
public:
    static void button_clicked(GtkWidget *button, gpointer data);
    static int delete_event(GtkWidget *widget,
                            GdkEvent *event, gpointer data);
private:
    static void do_message(const char*);
};
```

```cpp
void
callback::do_message(const char * msg)
{
    GtkWidget *dialogue;
    int ret;
    dialogue = gnome_message_box_new (
        "\nOK",
        NULL);
    ret = gnome_dialog_run (GNOME_DIALOG (dialogue));
}
```

```cpp
void
callback::button_clicked(GtkWidget *button, gpointer data)
{
    do_message((char*)data);
}
```

```cpp
/* 当用户关闭窗口时调用 */
gint
callback::delete_event(GtkWidget *widget, GdkEvent *event,
                       gpointer data)
{
    /* 信号主循环退出 */
    g_print("using C++ callback to quit\n");
    gtk_main_quit();
    /* 返回 FALSE 以继续关闭窗口 */
    return FALSE;
}
```

```cpp
int
main(int argc, char *argv[])
{
    GtkWidget *app;
    GtkWidget *button;
    GtkWidget *hbox;

    /* 初始化 GNOME，这非常类似于 gtk-* */
    gnome_init("buttons-basic-example", "0.1", argc, argv);

    /* 创建一个 Gnome app 控件，为你的应用程序设置一个基础窗口 */
    app = gnome_app_new("buttons-basic-example",
                        "Buttons");

    /* 绑定 *delete_event*，这是当我们通过窗口管理器关闭窗口时收到的事件
       用户通过窗口管理器关闭窗口，
       gtk_main_quit，这是一个导致 gtk main 主循环退出的函数，从而退出
       应用程序 */
    gtk_signal_connect (GTK_OBJECT (app), "delete_event",
                        GTK_SIGNAL_FUNC (callback::delete_event),
                        NULL);

    /* 为按钮创建一个水平框并将其添加到
       app 控件中 */
    hbox = gtk_hbox_new(FALSE, 5);
    gnome_app_set_contents(GNOME_APP (app), hbox);

    /* 创建一个按钮并将其添加到水平框中，
       并将点击事件绑定到 button_clicked */
    button = gtk_new_with_label("Button 1");
    gtk_box_pack_start (GTK_BOX(hbox), button, FALSE, FALSE, 0);
    gtk_signal_connect (GTK_OBJECT (button), "clicked",
                        GTK_SIGNAL_FUNC (callback::button_clicked),
                        "Button 1\n");

    /* 另一个按钮 */
    button = gtk_new_with_label("Button 2");
    gtk_box_pack_start (GTK_BOX(hbox), button, FALSE, FALSE, 0);
    gtk_signal_connect (GTK_OBJECT (button), "clicked",
                        GTK_SIGNAL_FUNC (callback::button_clicked),
                        "Button 2\n");

    /* 显示此 app 控件内部所有内容以及 app
       控件本身 */
    gtk_widget_show_all(app);

    /* 进入主循环 */
    gtk_main ();

    return 0;
}
```

### 2. 以最终的 wxWindows 或 KDE 示例为基础，扩展代码以显示一个文件浏览器按钮，该按钮允许你使用标准文件选择对话框选择文件。

你在 `ex26-02KDE.h` 中看到我们添加了一个额外的按钮变量 `m_btnBrowse`。我们在 `ex26-02KDE.cxx` 中通过新按钮来初始化它，并使用信号/槽机制将其连接到应用程序的 `SlotBrowse()` 处理器。在处理器中，我们使用静态成员函数 `QFileDialog::getOpenFileName(FileName(""))` 来打开标准的文件浏览对话框。注意，尽管我们的列表中没有这个文件，但我们 `#include "ex26KDE-01.moc"`。这是正常的，因为 MOC 在处理头文件时会为我们创建 `.moc` 文件。

# 练习题和测验答案
