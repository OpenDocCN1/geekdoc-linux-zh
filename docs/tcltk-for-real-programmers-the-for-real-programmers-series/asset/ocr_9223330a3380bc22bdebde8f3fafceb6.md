# Chapter 9. The canvas Widget, Images, and Events

```
# without causing the frame to resize itself.
# Because of this, the label can only have one ""
# in its name, and other "" are converted to "-"
# Arguments
# toolButtonName The full window name of a toolButton
# Results
# Returns the modified string
```

```
proc infoIdentifier {toolButtonName} {
    regsub -all {\.} $toolButtonName "-" infoID
    return $infoID
}
```

```
################################################################################
# proc cancelInfo {toolButtonName}--
# Cancels the scheduled display of an Info label
# Arguments
# toolButtonName The name of the toolbutton
# Results
# If this label was scheduled to be displayed,
#    it is disabled.
```

```
proc cancelInfo {toolButtonName} {
    variable after
    if {[info exists after({$toolButtonName})]} {
        after cancel $afters($toolButtonName);
    }
}
```

```
################################################################################
# proc scheduleInfo {name info} --
# Cancel any existing "after" scripts for this button.
# Arguments
```

314