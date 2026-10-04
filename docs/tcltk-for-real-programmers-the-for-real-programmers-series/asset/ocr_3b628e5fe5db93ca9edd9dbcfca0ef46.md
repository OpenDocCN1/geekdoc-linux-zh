# 14.3 Debugging

```
}
proc mean {lst {
  set sum [addList $lst]
  set count [length $lst]
  set mean [expr $sum / $count]
  return $mean
}
```

```
set lst [list 2 4 6 8]
entry .list -textvar lst
label .mean -textvar mean
button .go -Calculate mean" -command \
  {set mean [mean $lst]}
```

```
pack .list
pack .mean
pack .go
```

The application debugged is displayed in the upper left corner. The upper right-hand corner shows the TChoose window, which allows the user to select the application to debug and which procedures within that examination take. The window labeled TDebug-Backtrace shows the current stack. The window labeled TDebug-Widget-Hierarchy shows the names and types of this application's widgets.

The bottom window shows the code currently evaluated and the values of the local variables. I typed the command in the Eval entry widget to initialize the total variable to a bogus value, as shown in the Variables scrollbox.

# 14.3.2.3 ScriptTPro Debugger

| Language | executable |
|---|---|
| Primary Site | http://www.scriptics.com |
| Contact | sales@scriptics.com |
| Tcl Revision Supported | Tcl: 7.6-8.0 Tk: 4.2-8.0 |
| Supported Platforms | Unix, Windows NT, Windows 95 |