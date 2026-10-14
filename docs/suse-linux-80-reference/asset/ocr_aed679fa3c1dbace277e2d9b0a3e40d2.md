```
```text
INSTALL_DESKTOP_EXTENSIONS="yes"
```
```

Install the SuSE extensions for new users (theme and additional functions).

```
```text
KDM_SHUTDOWN="auto"
```
```

Specifies the users allowed to shut down or reboot the computer via kdm.  
Possible settings: root, all, none, local, and auto.

```
```text
KDM_USERS=""
```
```

Space-separated list of users for which icons should be shown in KDM. If  
empty, it uses system defaults.

```
```text
KDE_USE_FAM="no"
```
```

Should KDE use the fam daemon? It only makes sense on NFS mounted  
directories.

```
```text
KDE_USE_FAST_MALLOC="no"
```
```

Use the improved malloc? *Caution:* this way of allocating memory is still  
*experimental.*

```
```text
SUSEWM_UPDATE="yes"
```
```

Should SuSEConfig.fwm create system-wide configuration files for the win-  
dow managers?

```
```text
SUSEWM_WM="all"
```
```

Space-separated list of window managers for which configuration files  
should be generated.  Valid values are fvwm, fvwm2, fvwm95, bowman,  
wmw, ctwm, kwm, and all.

```
```text
SUSEWM_XPM="yes"
```
```

Set SUSEWM_XPM to yes for pixmaps in menus. package 3dpixms has  
to be installed.

# displaymanager — Display manager configuration

```
```text
DISPLAYMANAGER="kdm"
```
```

Set the display manager for login. Possible values: console, xdm (tradi-  
tional display manager of X Window System), kdm (display manager of  
KDE), gdm (display manager of GNOME) or wdm (“WINGs display man-  
ager”).

```
```text
DISPLAYMANAGER_REMOTE_ACCESS="no"
```
```

Allow remote access to your display manager (KDM only).

```
```text
DISPLAYMANAGER_STARTS_XSERVER="yes"
```
```

Display manager starts a local X server set to no for remote-access only.

# tetex — TeX/LaTeX.