```
bind $toolButtonName <Motion> \
    "[namespace current]::deleteInfo $toolButtonName";
bind $labelName <Motion> \
    "[namespace current]::deleteInfo $toolButtonName";
```

```
############################################################
# proc deleteInfo {toolButtonName} ---
# Deletes the label associated with this button, and
# resets the binding to the original actions.
# Arguments
# toolButtonName    The name of the parent button
#
# Results
# No more label, and bindings as they were before the
# mouse paused
# on this button
```

```
proc deleteInfo {toolButtonName} {
    variable binding
    set labelName \
        ".toolbutton_[infoIdentifier $toolButtonName]}"
    destroy $labelName;
    bind $toolButtonName <Motion> \
        $binding($toolButtonName);
}
```

# Example Script

```
frame .f
pack .f
toolbutton .f.b1 -info "B1 Message" -bitmap questhead \
    -command (puts "seeing head")
pack .f.b1 -side left
toolbutton .f.b2 -info "B2 Message" -bitmap question \
```