
```cpp
#include <kde/kaction.h>

KAction *openNew(const QObject *recvr, const char *slot, KActionCollection *

    parent,

const char *name = 0 )

KAction *save ...

KAction *saveAs ...

KAction *revert ...

KAction *close ...
```

## 使用 Qt 编程 KDE

```cpp
KAction * print ...
等...
```

每个标准动作都接收相同的参数：槽接收器和函数、一个 `KActionCollection` 以及 `KAction` 名称。`KActionCollection` 对象管理窗口中的所有 `KActions`，我们可以通过 `KMainWindow` 的 `KActionCollection` 方法获取当前对象。

```cpp
KAction *saveAs = KStAction::saveAs(this, SLOT(saveAs()), actionCollection(),
    "saveAs");
```

## 尝试一下——一个带有菜单和工具栏的 KDE 应用程序

```cpp
#include <kmainwindow.h>

class KDEMenu : public KMainWindow
(
    Q_OBJECT

public:

    KDEMenu(const char * name = 0);

    private slots:

    void newUser();

    void aboutApp();

};
```

- 2. 在 `KDEMenu.cpp` 中，我们从将要用部件的 `#include` 指令开始。

```cpp
#include <KDEMenu.h>

#include <kapp.h>

#include <kaction.h>

#include <kstaccel.h>

#include <kmenubar.h>

#include <kabout.h>
```

- 3. 在构造函数中，我们创建了三个 `KAction` 部件。`new_file` 使用手动定义创建的，而 `quit_action` 和 `help_action` 使用标准的 `KAction` 定义：

```cpp
KDEMenu::KDEMenu(const char *name = 0) : KMainWindow(
KAction *new_file = new KAction("New", "file", KStAccel::key(KStAccel::New),
    this, SLOT(new_file())), this, "newacion");

KAction *quit_action = KStAction::quit(KApplication(),
SLOT(quit()), actionCollection());

KAction *help_action = KStAction::about(this, SLOT(aboutApp()),
    actionCollection());
```

- 4. 我们创建了两个顶层菜单并将它们插入到 `KApplicationMenuBar` 中：

```cpp
QPopupMenu *file_menu = new QPopupMenu;

QPopupMenu *help_menu = new QPopupMenu;

menubar()->insertItem("&File", file_menu);

menubar()->insertItem("&Help", help_menu);
```

- 5. 现在我们将动作插入菜单和工具栏中，在 `new_file` 和 `quit_action` 之间插入了一条分割线：

```cpp
new_file->plug(file_menu);

file_menu->insertSeparator();

quit_action->plug(file_menu);

help_action->plug(help_menu);

new_file->plug(toolBar);

quit_action->plug(toolBar);

}
```

- 6. 最后是一些槽函数的定义：`about` 创建了一个 `KAbout` 来显示关于程序的信息。注意 `quit` 槽被定义为 `KApplication` 的一部分。

```cpp
void KDEMenu::newFile()

{
  // 创建新文件
}

void KDEMenu::aboutApp()

{
  KAboutDialog *about = new KAboutDialog(this, "dialog");

  about->setAuthor(QString("A. N. Author"), QString("email.net"));

  about->setUrl(QString("http://url.com"), QString("work"));

}
```

# 第 17 章

5. 接下来是 `QListView` 小部件，它占据了窗口的大部分区域。然后我们将必要的信号连接到我们的 `doSearch` 槽以执行 CD 数据库搜索。通过添加一条空消息，`KMainWindow` 的状态栏变得可见。

```cpp
list = new QListView(vbox, "name", OL);

list->setRootIsDecorated(TRUE);

list->addColumn("Title");

list->addColumn("Artist");

list->addColumn("Catalog");

connect(button, SIGNAL(clicked()), this, SLOT(doSearch()));

connect(search_entry, SIGNAL(returnPressed()), this, SLOT(doSearch()));

statusBar()->message("");

setCentralWidget(vbox);

resize(300,400);
```

6. `doSearch` 是应用程序的核心。它读取搜索字符串并获取所有匹配的 CD 及其音轨。逻辑与第 16 章中 GNOME/GTK+ 的 `doSearch` 函数相同。

```cpp
void MainWindow::doSearch()

{
    cd_search_st *cd_res = new cd_search_st;

    current_cd_st *cd = new current_cd_st;

    struct current_tracks_st ct;

    int res1, i, j, res2, res3;

    char track_title[110];

    char search_text[100];

    char statusBar_text[200];

    QListViewWidgetItem *cd_item;

    strcpy(search_text, search_entry->text());
```

7. 获取 CD ID 并更新状态栏以显示搜索结果。

8. 对于每个 ID，获取 CD 信息，插入 `QListView` 并获取该 CD 的所有音轨。

```cpp
while (i < res1) {
    res2 = get_cd(cd_res->cd_id[i], cd);
    cd_item = new QListWidgetItem(list, cd->title, cd->artist_name, cd->catalogue);
    res3 = get_cd_tracks(cd_res->cd_id[i++], &ct);
    j = 0;
    /* 用当前 cd 的音轨填充树结构 */
    while (j < res3) {
      sprintf(track_title, " Track %d. ", j+1);
      strcat(track_title, ct.track[j++]);
      new QListWidgetItem(cd_item, track_title);
    }
}
```

9. 当 `addcd_action` 菜单项或工具栏按钮激活时，会调用 `AddCd` 槽。

```cpp
void MainWindow::AddCd()

{
  AddCdDialog *dialog = new AddCdDialog(this);
  dialog->show();
}
```

结果如图 17-13 所示。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_756_0.png)

图 17-13

# 尝试一下—AddCdDialog

为了添加 CD，我们需要编写包含所需输入字段的对话框。

- 1. 输入以下内容并命名为 `AddCdDialog.h`。注意 `AddCdDialog` 继承自 `KDialogBase`，这是 KDE 的对话框小部件。

```cpp
#include <kdialogbase.h>

#include <qlineedit.h>
```

```cpp
class AddCdDialog : public KDialogBase
{
    Q_OBJECT

public:
    AddCdDialog(QWidget *parent);

private:
    QLineEdit *artist_entry, *title_entry, *catalogue_entry;

public slots:
    void okClicked();

};
```

- 2. 接下来是 `AddCdDialog.cpp`，它在 `okClicked` 槽中调用 MySQL 接口代码中的 `add_cd` 函数：

```cpp
#include "AddCdDialog.h"

#include "mysql.h"

#include <layout.h>

#include <label.h>

AddCdDialog::AddCdDialog(QWidget *parent)
    : KDialogBase(parent, "AddCD", false, "Add CD",
      KDialogBase::Ok|KDialogBase::Cancel, Ok, true)
{
    QWidget *widget = new QWidget(this);

    setMainWidget(widget);

    QGridLayout *grid = new QGridLayout(widget,3,2,10,5,"grid");
    grid->addWidget(new QLabel("Artist", widget, "artistlabel"), 0, 0, 0);
    grid->addWidget(new QLabel("Title", widget, "titlelabel"), 1, 0, 0);
    grid->addWidget(new QLabel("Catalogue", widget, "cataloguelabel"), 2, 0, 0);

    artist_entry = new QLineEdit(widget, "artist_entry");
    title_entry = new QLineEdit(widget, "title_entry");
    catalogue_entry = new QLineEdit(widget, "catalogue_entry");

    grid->addWidget(artist_entry, 0, 1, 0);
    grid->addWidget(title_entry, 1, 1, 0);
    grid->addWidget(catalogue_entry, 2, 1, 0);

    connect(this, SIGNAL(okClicked()), this, SLOT(okClicked()));
}

void AddCdDialog::okClicked()
{
    char artist[200];
    char title[200];
    char catalogue[200];
    int cd_id = 0;

    strcpy(artist, artist_entry->text());
    strcpy(title, title_entry->text());
    strcpy(catalogue, catalogue_entry->text());

    add_cd(artist, title, &cd_id);
}
```

图 17-14 显示了 `AddCdDialog` 的运行效果。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_758_0.png)

图 14

# 尝试一下—LogonDialog

当然，在登录之前无法查询数据库，因此我们需要一个简单的对话框来输入凭据。我们将此类称为 `LogonDialog`（巧妙的名字！）。

- 1. 首先是头文件。输入此内容并为 `LogonDialog`。注意这次我们继承自 `QDialog` 而不是 `KDialogBase`。

```cpp
#include <qdialog.h>

#include <qlineedit.h>

class LogonDialog : public QDialog
{
    Q_OBJECT

public:
    LogonDialog(QWidget *parent = 0, const char *name = 0);

    QString getUsername();

    QString getPassword();

private:
    QLineEdit *username_entry, *password_entry;
};
```

- 2. 与在 `LogonDialog.cpp` 中封装 `database_start` 调用相比，我们有了用户名和密码的方法。这里是 `LogonDialog.cpp`：

```cpp
#include "LogonDialog.h"

#include "app_mysql.h"

#include <qpushbutton.h>

#include <qlayout.h>

#include <qlabel.h>

LogonDialog::LogonDialog(QWidget *parent, const char *name) : QDialog(parent, name)
{
    QGridLayout *grid = new QGridLayout(this, 3, 2, 10, 5, "grid");
    grid->addWidget(new QLabel("Username", this, "usernamelabel"), 0, 0, 0);
    grid->addWidget(new QLabel("Password", this, "passwordlabel"), 1, 0, 0);

    username_entry = new QLineEdit(this, "username_entry");
    password_entry = new QLineEdit(this, "password_entry");
    password_entry->EchoMode(QLineEdit::Password);

    grid->addWidget(username_entry, 0, 1, 0);
    grid->addWidget(password_entry, 1, 1, 0);

    QPushButton *button = new QPushButton("Ok", this, "button");
    grid->addWidget(button, 2, 1, Qt::AlignRight);
    connect(button, SIGNAL(clicked()), this, SLOT(accept()));
}

QString LogonDialog::getUsername()
{
    if (username_entry == NULL)
        return QString("");
    return username_entry->text();
}

QString LogonDialog::getPassword()
{
    if (password_entry == NULL)
        return QString("");
    return password_entry->text();
}
```

图 17-15 显示了对话框的样子。

![](img/5142272414a3a6a6c81e4d1e9d75bbc1_759_0.png)

图 17-15

# 尝试一下—main.cpp

剩下的代码是 `main` 函数，我们将其放在单独的文件 `main.cpp` 中。

- 1. 在 `main.cpp` 中，我们打开 `LogonDialog` 并通过 `database_start` 获取成功登录。如果登录失败，我们显示一个 `MessageBox`；如果尝试退出 `LogonDialog`，则询问用户是否想要退出。

```cpp
#include "MainWindow.h"

#include "app_mysql.h"

#include "LogonDialog.h"

#include <application.h>
```
