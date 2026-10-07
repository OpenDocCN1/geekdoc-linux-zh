```
"ddraw" = "builtin, native"
"dinput" = "builtin, native"
"dsound" = "builtin, native"
"mmsystem" = "builtin"
"winmm" = "builtin"
"msvcrt" = "native, builtin"
"msvideo" = "builtin, native"
"mswf32.drv" = "builtin, native"
"mcida.drv" = "builtin, native"
"mciseq.drv" = "builtin, native"
"mciwave.drv" = "builtin, native"
"mciavi.drv" = "native, builtin"
"mcianim.drv" = "native, builtin"
"msacm.drv" = "builtin, native"
"msacm" = "builtin, native"
"msacm32.drv" = "builtin, native"
"midip32.drv" = "builtin, native"
"wnaspi32" = "builtin"
"icmp" = "builtin"
```

# CAUTION

If you use dll overrides or otherwise experiment with Wine, always back up a copy of the original
configuration file.

```
[x11drv]
; Number of colors to allocate from the system palette
; AllocSystemColors = "100"
; Use a private color map
; PrivateColorMap = "N"
; Favor correctness over speed in some graphics operations
;PerfectGraphics = "N"
; Color depth to use on multi-depth screens
;;;ScreenDepth = "16"
```

Wine displays the Windows application output in a desktop window in display :0.0.
Changing the default display from :0.—which represents the default X11 port number
(6000) and the session's first screen (0)—can be helpful when Wine is used to remotely
display applications over a network or used on a PC with multiple video cards in order to have programs automatically appear on a specific monitor.

```
; Name of X11 display to use
;;"Display" = ":0.0"
```