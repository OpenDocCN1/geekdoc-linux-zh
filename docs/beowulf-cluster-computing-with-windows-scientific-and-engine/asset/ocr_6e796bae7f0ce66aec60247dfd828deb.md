```
```c
pvm_initsend( PvmDataDefault );
pvm_pkinf( &kin, 1, 1 );
pvm_send( cc, CNTR_MSGTAG );
incr += 2;
/* Check Ack from Master */
pvm_recv( cc, CNTR_MSGTAG );
pvm_upkinf( &ack, 1, 1 );
} while ( ack > 0 );
}
```
pvm_exit();
return( 0 );
}
```
```

In a typical message-passing system, messages are transient, and the focus is on making their existence as brief as possible by decreasing latency and increasing bandwidth. But there are a growing number of situations in the parallel applications seen today in which programming would be much easier if there was a way to have persistent messages. This is the purpose of the *Message Box* feature in PVM. The Message Box is an internal tuple space in the virtual machine.

Four functions make up the Message Box:

```
index = pvm_putinfo( name, msgbuf, flag )
\tpvm_recvinfo( name, index, flag )
\tpvm_delinfo( name, index, flag )
\tpvm_getboxinfo( pattern, matching_names, info )
```

Tasks can use regular PVM pack routines to create an arbitrary message and then use pvm_putinfo() to place this message into the Message Box with an associated name. Copies of this message can be retrieved by any PVM task that knows the name. If the name is unknown or is changing dynamically, then pvm_getboxinfo() can be used to find the list of names active in the Message Box. The flag defines the properties of the stored message, such as who is allowed to delete this message, whether this name allows multiple instances of messages, and whether a put to the same name can overwrite the message.

The Message Box has been used for many other purposes. For example, the PVM group server functionality has all been implemented in the new Message Box functions; the Cumnivs computational steering tool uses the Message Box to query for the instructions on how to attach to a remote distributed simulation; and performance monitors leave their findings in the Message Box for other tools to use.