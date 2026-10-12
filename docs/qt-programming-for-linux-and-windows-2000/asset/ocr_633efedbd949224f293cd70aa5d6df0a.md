Always check the return from the `new` operator with a subsequent call to the Qt `CHECK_PTR()` macro. A bug in an object's constructor or a resource or quota problem can be very difficult to locate otherwise. The following example demonstrates a possible convention to use.

```
```
QLabel *1 = new QLabel( this );
CHECK_PTR( 1 );
```
```

# Use Slots For Exposed void-return Methods

Declaring an access specifier on a class method as "<access> slot;" has no associated performance cost if the method is called as a normal class method. There is a very small resource cost incurred within the text (or code) segment, and a very minor performance cost if the method is invoked via emit. Since the signal/slot mechanism is totally independent of the GUI event loop, the use of signals and slots doesn't mean your object must be used in a GUI application.

Consider the following code fragment:

```
```
class MyObject : public QObject
{
 Q_OBJECT
public:
 MyObject( QObject *p=0 );
 const QString &text();
 void nonSlotSetText( const QString &s ) { data = s; }

public slots:
 void setText( const QString &s ) { data = s; }

private:
 QString data;
};
```
```

In this example, the nonSlotSetText() method will perform no better (or worse) than the setText() slot method, when called as a normal class method. The only real difference is that the nonSlotSetText() method cannot be connected to another object's signal. Therefore, it makes sense to expose reusable components' public or protected void-return methods as slots, whether you can foresee a need to connect them to a signal or not.

# DYNAMIC AND STATIC LINKAGE

Almost every modern operating system has adopted the concept of *dynamic* (or shared) libraries of routines. On Linux platforms, these are usually denoted by a .so.Major.Minor suffix on an executable file, reminiscent of the Sun Microsystems naming convention. On