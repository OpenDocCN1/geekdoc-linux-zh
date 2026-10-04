# 9.6 Creating a Widget

Putting the scheduleInfo, cancelInfo, createInfo, and deleteInfo commands into a namespace protects these commands from possible collision with other commands and does not pollute the global space. Creating these procedures inside the namespace also allows them to create and share the associative arrays after and binding without exposing these arrays to procedures outside this namespace.

Example 9.6-1

```
####################################################################
# proc tooltip {toolButtonName args}-
# Create a button icon that will evaluate a command when
# clicked
# and display an information label if the cursor rests on it
#
# Arguments
# toolButtonName      The name of this button
# args                A list of -flag value pairs
#
# Results
# Creates a new button and returns the name to the
# calling script
# Throws an error if unrecognized arguments or required args
# are missing.
#
proc tooltip {toolButtonName args} {
    # These arguments are required.
    set reqOptions [list -command -info -bitmap]

    # Check that the required arguments are present
    # Throw an error if any are missing.
    foreach required $reqOptions {
        if [[lsearch -exact $args $required] < 0]} {
            error "tooltip requires a $required option"
        }
    }

    # define defaults
    set height 32
    set width 32
```