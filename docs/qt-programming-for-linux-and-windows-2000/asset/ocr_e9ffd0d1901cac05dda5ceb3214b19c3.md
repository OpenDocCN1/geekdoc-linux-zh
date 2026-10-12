```
QTimer *t new QTimel( this, false );
```

# Common Use

```
/ / We need a flashing text label, so we subclass QLabel and
/ / add a QTimer. We tried to tell the customer it uses a lot
/ / of resources…
class Blinky : public QLabel
{
   Q_OBJECT
public:
   Blinky( QWidget *p=0, const char *n=0 );
   Blinky( const QString &s, QWidget *p=0, const char *n=0 );

public slots:
   void setValue( const QString &s );

protected slots:
   void myTimeout();

private:
   QLabel *l;
   QString &str;
   bool showing;
};

/ / Convenience ctor sets the label text and saves a copy
Blinky:: Blinky( const QString &s, QWidget *p, const char *n )
{
   QLabel( s, p, n )
   str = s;
}

/ / Standard constructor adds the timer
Blinky:: Blinky( QWidget *p, const char *n )
{
   Blinky( ":", p, n );
   showing = true;
   tnr = new QTuner( this );
   connect( tnr, SIGNAL(timeout( ) ), SLOTCmyTineout()) );
   t -> start( 500 );
}

/ / A slot to set the text value
void
Blinky:: setValue( const QString &s )
{
   setText( s );
   str = s;
}
```