
## Table 2.3 (Continued)

| Public Members | Purpose |
| :--- | :--- |
| `bool inherits( const char * )` | Returns true if this object instance inherits the argument class type |
| `const char * name()` | Returns the instance name of this object |
| `const char * name( const char * )` | Returns the instance name of this object if one exists, otherwise the argument is assigned as the new instance name |
| `virtual void setName( const char * )` | Sets the instance name of this object |
| `bool isWidgetType()` | Returns true if this object is a widget |
| `bool highPriority()` | Returns true if this object is a high priority object |
| `bool signalsBlocked()` | Returns true if signals are blocked by this object |
| `void blockSignals( bool b )` | Enables/disables blocking of signals by this object |
| `int startTimer( int )` | Starts a timer with a period equal to the argument number of milliseconds. It returns a timer ID |
| `void killTimer( int )` | Stops the timer with the argument ID |
| `void killTimers()` | Stops all timers associated with this object |
| `QObject * child( const char *name, const char *type = 0 )` | Returns a pointer to the object with the specified name and type, NULL otherwise |
| `const QObjectList * children()` | Returns a pointer to the list of children of this object |
| `QObjectList * queryList( const char * inherit=0, const char *name=0, bool regexMatch=true, bool recursiveSearch=true )` | Permits regular expression searches for specific objects. It returns a pointer to the list of matching objects |
| `virtual void insertChild( QObject * )` | Inserts the specified argument as a child of this object |
| `virtual void removeChild( QObject * )` | Removes the specified object from this object's tree |
| `void installEventFilter( const QObject * )` | Installs an event filter for this object |
| `void removeEventFilter( const QObject * )` | Removes the event filter from this object |

## Table 2.3 (Continued)

| Public Members | Purpose |
| :--- | :--- |
| `bool connect( const QObject *sender, const char *signal, const char *member )` | Connects the signal from the sender object to the member slot. Returns true on success, false on failure |
| `bool disconnect( const char *signal=0, const QObject *receiver=0, const char *member=0 )` | Disconnects the signal that is connected to the member slot of the receiver object. Returns true on success, false on failure |
| `bool disconnect( const QObject *receiver, const char *member=0 )` | Disconnects all signals that are connected to the member slot of the receiver object. Returns true on success, false on failure |
| `void dumpObjectTree()` | Very useful for debugging. Dumps the object tree structure to the debugging output (stderr on Linux, application console on Windows (requires that Qt be built with debugging enabled) |
| `void dumpObjectInfo()` | Very useful for debugging. Dumps the object information (slot connections, etc.) to the debugging output (stderr on Linux, application console on Windows (requires that Qt be built with debugging enabled) |
| `bool setProperty( const char *name, const QVariant &value )` | Sets object's property name to the argument value. Returns true on success, false on failure |
| `QVariant property( const char * )` | Returns the specified property from the object |
| `QObject * parent()` | Returns a pointer to the object's parent object or NULL if no parent exists |

### Static Public Members

| Members | Purpose |
| :--- | :--- |
| `QString tr( const char * )` | Returns a translated version of the argument string or the argument string if no translation exists |
| `const QObjectList * objectTrees()` | Returns a pointer to a list of all of the object's object trees |
| `bool connect( const QObject *sender, const char *signal, const QObject *receiver, const char *member )` | Connects the sender object's signal to the receiver object's member slot. Returns true on success, false on failure |
| `bool disconnect( const QObject *sender, const char *signal, const QObject *receiver, const char *member )` | Disconnects the sender object's signal from the receiver object's member slot. Returns true on success, false on failure |

### Protected Members

| Members | Purpose |
| :--- | :--- |
| `QConnectionList * receivers( const char * )` | Returns a pointer to an array of object/slot pairs for the argument signal or zero if the signal is not connected to anything |
| `const QObject * sender()` | Returns a pointer to the last object that sent a signal to this object |
| `virtual void initMetaObject()` | Enables the meta object associated with this object. This is performed on demand |
| `virtual void timerEvent( QTimerEvent * )` | Reimplement this method in a subclass to receive timer events |
| `virtual void childEvent( QChildEvent * )` | Reimplement this method in a subclass to receive child events (events are sent when child objects are inserted or removed) |
| `virtual void connectNotify( const char * )` | This method is called when the argument signal has been connected to a slot |
| `virtual void disconnectNotify( const char * )` | This method is called when the argument signal has been disconnected from a slot |
| `virtual bool checkConnectArgs( const char *sig, const QObject *receiver, const char *member )` | Returns true if the sig can be connected to the receiver object's member slot, false otherwise |

### Static Protected Members

| Members | Purpose |
| :--- | :--- |
| `QMetaObject * staticMetaObject()` | Enables the meta object associated with this object. This is performed on demand. Identical to initMetaObject() but reimplemented as a static method |

## Signals and Slots vs. Callbacks

Any GUI application that provides user interaction (as well as many applications that don't) relies to some extent on events or messages that will trigger the execution of code that will (hopefully) deal with the specific event or message. For X11 applications, these are commonly referred to as *events*, while the Windows-speak term is *messages*. The term is irrelevant but the concept is pretty much the same. The methods used to deal with them differ somewhat between the two architectures.

Applications based on the X11 Toolkit, Xi (Motif and friends), use *callback* functions that accept arguments specific to the widget or to the event they are intended to handle. These callback functions must be registered with Xi for each widget that will make use of the particular callback, and it's the programmer's responsibility to guarantee that the argument lists will match at runtime. Since there is very little (or no) type-checking performed at compile-time, there is no guarantee that the callback function's arguments will be set as the programmer intended. If you make a mistake and if you are very lucky, the program will crash and you will have a core file or some debug information to help you find the problem in your code. More often than not, unfortunately, the program will behave erratically and you'll spend more time tracking it down. Whatever the result, a lot more time is spent debugging these applications than would otherwise be required if these connections were *type-checked*.

The Microsoft Foundation Class library, or *MFC*, uses compile-time macros and message maps to connect messages to C++ methods. Neither C nor C++ compilers can type-check a macro so MFC provides no benefits in this respect over the callback approach for Motif. MFC also requires the programmer to provide a rather complex message map that is as difficult to read as it is to write. This issue is usually dealt with by using the sophisticated Microsoft or Borland IDEs and their visual design tools. I won't speculate on Microsoft's reasons for creating a dependence on Microsoft tools and neither should you.

Qt addresses all these issues with an elegant alternative. Qt objects and objects that you create can *emit* (or send) signals without knowing what object(s) will receive them. Qt objects can also provide slots to receive signals emitted by other objects without knowing anything about the object that emitted the signal. This is a big improvement over the other methods discussed above, and presents some unique problems of its own that will be discussed a little later.

## Signals
Don't confuse Qt signals or Linux or UNIX signals! They have nothing to do with one another.

Qt signals are sent by Qt objects or objects you create. The object emits the signal and doesn't care who, if anyone, receives the signal. An object may emit a signal to notify that the mouse has been moved or that a value has changed. Not having to know anything about who will use the object eliminates the need to anticipate the intended use of that object, and this supports a component model of development that encourages reuse of existing code.

## Slots
Qt objects and objects you create can provide special functions known as *slots*. Slot functions are special because signals that are emitted by any Qt object can be connected to, or disconnected from, these slot functions using the QObject::connect() and QObject::disconnect() methods. The only constraint on the connections is that the type of the signal must match the type of the slot. If you have ever performed any electronic “breadboarding,” a method of electronic prototyping that's very component-oriented, the
