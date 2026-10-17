
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

2. 接下来是 `AddCdDialog.cpp`，它在 `okClicked` 槽中调用 MySQL 接口代码中的 `add_cd` 函数：

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

## 尝试一下—`LogonDialog`

当然，在登录之前无法查询数据库，因此我们需要一个简单的对话框来输入凭据。我们将此类称为 `LogonDialog`（巧妙的名字！）。

1. 首先是头文件。输入此内容并保存为 `LogonDialog.h`。注意这次我们继承自 `QDialog` 而不是 `KDialogBase`。

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

2. 与在 `LogonDialog.cpp` 中封装 `database_start` 调用相比，我们有了用户名和密码的方法。这里是 `LogonDialog.cpp`：

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

## 尝试一下—`main.cpp`

剩下的代码是 `main` 函数，我们将其放在单独的文件 `main.cpp` 中。

1. 在 `main.cpp` 中，我们打开 `LogonDialog` 并通过 `database_start` 获取成功登录。如果登录失败，我们显示一个 `MessageBox`；如果尝试退出 `LogonDialog`，则询问用户是否想要退出。

```cpp
#include "MainWindow.h"
#include "app_mysql.h"
#include "LogonDialog.h"

#include <application.h>
#include <qbox.h>

int main(int argc, char **argv) {
    char username[100];
    char password[100];

    QApplication a(argc, argv, "cdapp");
    LogonDialog *dialog = new LogonDialog();
}
```
