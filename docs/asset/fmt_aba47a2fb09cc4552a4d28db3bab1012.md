
```cpp
case QMessageBox::No:
    label->setText(QString("No"));
    break;
}
}
```

```cpp
void Mboxes::button4()
{
    int result = QMessageBox::warningContinueCancel(this,
        "Overwrite the existing file?",
        "warningContinueCancel",
        QString("Overwrite"));
    switch(result) {
        case QMessageBox::Continue:
            label->setText(QString("Continue"));
            break;
        case QMessageBox::Cancel:
            label->setText(QString("Cancel"));
            break;
    }
}
```

```cpp
void Mboxes::button5()
{
    int result = QMessageBox::warningYesNoCancel(this,
        "Quitting without saving the file\n"
        "loss of data. Save before quitting?",
        "warningNoCancel");
    switch(result) {
        case QMessageBox::Yes:
            label->setText(QString("Yes"));
            break;
        case QMessageBox::No:
            label->setText(QString("No"));
            break;
        case QMessageBox::Cancel:
            label->setText(QString("Cancel"));
            break;
    }
}
```

```cpp
void Mboxes::error()
{
    QMessageBox::critical(this, "Error", "Unable to save configuration.");
}
```

```cpp
void Mboxes::sorry()
{
    QMessageBox::warning(this, "Sorry", "The file specified contains no data.");
}
```

```cpp
void Mboxes::information()
{
    QMessageBox::information(this, "Information", "Pressing Esc will clear the window.");
}
```

```cpp
void Mboxes::about()
{
    QMessageBox::information(this, "About", "Pressing Esc will clear the window.");
}
```

该类的定义为每个九个按钮中的每一个都包含了一个槽，并包含了放置在显示底部的标签。

## Mboxes

```cpp
/* mboxes.cpp */
#include "mboxes.h"
#include <qpushbutton.h>
#include <qmessagebox.h>
#include <qlayout.h>

Mboxes::QWidget(QWidget *parent, const char *name)
    : QWidget(parent, name)
{
    QPushButton *button;
    QVBoxLayout *layout = new QVBoxLayout(this);
    button = new QPushButton("Question Yes No", this);
    layout->addWidget(button);
    connect(button, SIGNAL(clicked()), this, SLOT(button1()));
    button = new QPushButton("Question Yes No List", this);
    layout->addWidget(button);
    connect(button, SIGNAL(clicked()), this, SLOT(button2()));
    button = new QPushButton("Warning Yes No", this);
    layout->addWidget(button);
    connect(button, SIGNAL(clicked()), this, SLOT(button3()));
    button = new QPushButton("Warning Continue Cancel", this);
    layout->addWidget(button);
```
