+   * The remaining characters are numeric in the range 0 to 9
+   * Provides a Boolean test for validity
+   * Produces a notification when validity changes state, suitable for connect to a QButton::setEnabled( bool ) slot (e.g., an OK button)
+   * Value can be set programmatically
+   * Invalid input is not accepted
+   * A lowercase leading alpha will be capitalized automatically

```
#ifdef _PARTNUMH
#define _PARTNUMH

#include <qlineedit.h>
#include <ctype.h>

class PartNum : public QLineEdit
{
  Q_OBJECT
public:
  PartNum( QWidget *p=0, const char *n=0 );
  virtual PartNum();

  bool       isValid( { return _valid } );

signals:
  // We'll emit this whenever the validity
  // changes
  void       valid( bool );

protected slots:
  // This slot will perform all the input
  // validation
  virtual void verify( const QString & );

private:
  bool       _valid;
};

PartNum.h

#include <PartNum.h>

PartNum::PartNum( QWidget *parent,
                   const char *name )
  : QLineEdit( parent, name )
{
  _valid = false;
  connect( this,
           SIGNAL(textChanged( const QString & ) ),
           SLOT(verify( const QString & ) ) );

```