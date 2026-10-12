```
left->setAlignment( AlignVCenter|AlignRight );
top->addWidget( left );
// val displays the value in the pair
val = new QLabel( this );
top->addWidget( val );
}
#include "NewW.moc"
```

OK, we have a new widget. It exposes all the same methods, signals, and slots as a QWidget, adding two new slots in the process. Internally, it maintains a layout and two label widgets, but you needn't concern yourself with how the management is accomplished---for the purpose of this discussion, it just is.

Now, we'll make use of our new widget. We'll create two instances of NewWidget and delete one when the user clicks a button, then we'll discuss what you can expect to happen:

main.cpp

```
#include "NewW.h"
#include <qapplication.h>
#include <qpushbutton.h>

class screen : public QWidget
{
    Q_OBJECT
public:
    screen();
protected slots:
    void delbot() { delete bottom, bottom = 0; }
private:
    NewWidget *above, *bottom;
};

screen::screen()
    : QWidget( 0, 0 )
{
    // Vertical layout---two NewWidgets and a button
    QVBoxLayout *top = new QVBoxLayout( this );
    above = new NewWidget( this );
    above->setLabel( "Upper Value:" );
    above->setValue( "Above it all" );
    top->addWidget( above );
    bottom = new NewWidget( this );
    bottom->setLabel( "Lower Value:" );
    bottom->setValue( "Bottomed-out" );
    top->addWidget( bottom );
    QPushButon *pb = new QPushButton( "Delete Bottom", this );
    connect(pb, SIGNAL(clicked()), SLOT(delbot()));
}
```