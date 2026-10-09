| Library routine | Command | Use |
| --- | --- | --- |
| odm.set_path |  | Set ODM database location (ODMDIR represents a shell environment variable) |
|  | RESTBASE | Retrieve customized objects from boot image and store in ODM |
|  | SAVEBASE | Store ODM-customized objects in boot image |
| odm.rm_class | ODMDROP | Remove an object class |
|  | ODMSHOW | Display object class definition |
| odm.create_class | ODMCREATE | Create empty object class with associated C headers for applications |
| odm.add_obj | ODMADD | Add an object to an object class |
| odm.change_obj | ODMCHANGE | Modify object attributes |
| odm.rm_obj | ODMDELETE | Delete object from an object class |
| odm.get_obj | ODMGET | Retrieve an object in odmdat format |
| odm.get_by_id |  | Retrieve an object by its ID |
| odm.rm_by_id |  | Remove an object by its ID |
| odm.get_first |  | Retrieve first object that matches criteria |
| odm.get_next |  | Retrieve next object that matches criteria |
| odm.get_list |  | Retrieve a list of objects that match criteria |
| odm.mount_class |  | Retrieves the class symbol structure |
| odm.open_class |  | Open an object class |
| odm.free_list |  | Free memory allocated for odm.get_list |
| odm.run_method |  | Execute method associated with an object |
| odm.close_class |  | Close object class |
| odm.err_msg |  | Retrieve error message string |
| odm.lock |  | Lock object for update |
| odm.unlock |  | Unlock object |
| odm.initialize |  | Initialize ODM session |
| odm.terminate |  | Terminate an ODM session |

Table 9-1. ODM Commands and Library Subroutines

| Command | Action |
| --- | --- |
| # smitty devices | SMIT FastPath |
| # mkdev -I tty 0 | Add a TTY device |
| # lsdv -C -s ascii -H | List existing SCSI devices |
| # chdev -l rmt 0 -a block_size = 0 | Change tape block size |
| # leattr -D -l rmt 0 | List tape attributes |
| # rmdev -I rmt 0 | Turn off the tape device but keep the definition |
| # rmdev -l rmt 0 -d | Remove a tape device |
| # cfcmgr | Update ODM and kernel |

Table 9-2. Most Common ODM Commands