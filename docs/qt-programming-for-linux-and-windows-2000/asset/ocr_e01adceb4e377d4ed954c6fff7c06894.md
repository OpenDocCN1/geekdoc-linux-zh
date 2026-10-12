# Table 2.3 (Continued)

| **Static Public Members** | **Purpose** |
| :--- | :--- |
| bool disconnect( const QObject \*sender,\nconst char \*signal,\nconst QObject \*receiver,\nconst char \*member ) | Disconnects the sender object's signal from the receiver object's member slot. Returns true on success, false on failure |

| **Protected Members** | **Purpose** |
| :--- | :--- |
| QConnectionList *\nreceivers( const char * ) | Returns a pointer to an array of object/slot pairs for the argument signal or zero if the signal is not connected to anything |
| const QObject *\nsender() | Returns a pointer to the last object that sent a signal to this object |
| virtual void\ninitMetaObject() | Enables the meta object associated with this object. This is performed on demand |
| virtual void\ntimerEvent( QTimerEvent * ) | Reimplement this method in a subclass to receive timer events |
| virtual void\nchildEvent( QChildEvent * ) | Reimplement this method in a subclass to receive child events (events are sent when child objects are inserted or removed) |
| virtual void\nconnectNotify( const char * ) | This method is called when the argument signal has been connected to a slot |
| virtual void\ndisconnectNotify( const char * ) | This method is called when the argument signal has been disconnected from a slot |
| virtual bool\ncheckConnectArgs( const char \*sig,\nconst QObject \*receiver,\nconst char \*member ) | Returns true if the sig can be connected to the receiver object's member slot, false otherwise |

| **Static Protected Members** | **Purpose** |
| :--- | :--- |
| QMetaObject *\nstaticMetaObject() | Enables the meta object associated with this object. This is performed on demand. Identical to initMetaObject() but reimplemented as a static method |

# Signals and Slots vs. Callbacks

Any GUI application that provides user interaction (as well as many applications that don't) relies to some extent on events or messages that will trigger the execution of code that will (hopefully) deal with the specific event or message. For X11 applications, these