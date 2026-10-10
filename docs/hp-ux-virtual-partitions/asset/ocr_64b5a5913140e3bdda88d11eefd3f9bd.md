```
```
keyword value
}
```
```

Note that all definitions have the following general syntax:
`KEYWORD value`

Notice that a data type definition is actually in two parts: an attribute part and a criteria part. The attribute portion of the data type definition specifies the look of the datatype; the criteria portion specifies the behavior of the data type.

For example, here's a file type for FrameMaker files that uses the FRAME action:

```
``` 
DATA_ATTRIBUTES       FRAME_Docs
                    {
                        DESCRIPTION This file type is for FrameMaker documents
                        ICON        makerIcon
                        ACTIONS     FRAME
                    }

DATA_CRITERIA         {
                        DATA_ATTRIBUTES_NAME FRAME_Docs
                        NAME_PATTERM      *.fm
                        MODE      f
                    }
```
```

You can create actions and file types from scratch using these formats. However, the easiest way to create an action is to use the **CreateAction** tool. *CreateAction* is located in the Desktop Applications folder of the Applications Manager and presents you with a fill-in-the-blank dialog box that guides you through creating an *action.dt* file containing the action definition. You can then move this file to the appropriate directory for the range of influence you want the action to have: */etc/dt/appconfig/types* for a system-wide influence; *$HOME/.dt/types* for individual users.

# Creating a New Icon and Action

Creating an icon is a challenging task. We could use the Icon Editor found in Desktop_Apps to create a new icon, or we could find a picture we like and