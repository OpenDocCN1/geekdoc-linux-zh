Manager uses these internal descriptions and the current system state to display on your desktop just those elements that will fit and that aren’t covered by other features as part of the screen rasterization process.

| COMMAND NAME | DESCRIPTION |
| --- | --- |
| Shuffle Up | Moves a window from back to front. |
| Shufle Down | Moves a window from front to back. |
| Refresh | Redraws your screen, which is useful if an application leaves a screen artifact behind. |
| Clean Up Icons | Moves your icons to a row and column display if you have the option set for window behavior to leave icons in the window where you place them. |
| Minimize/Restore Front Panel | Changes the front panel to an icon or restores it to its expanded size. |
| Restart Workspace Manager | Closes the Workspace Manager and restarts it with its last saved settings. This command is useful if you experience an application error and don’t want to restart your entire system and lose unsaved work. You should also use this command if you lose the title bar off of your desktop by inadvertently repositioning it. |
| Update Workspace Menu | Refreshes the Workspace menu; useful if you have modified the front panel in any way. |
| Disable Access Control | Turns off any keyboard or beep behavior you have set in the AccessX control that is found in the Desktop_Control’s folder. |
| Enable Access Control | Reestablishes the settings you have in the AccessX control. |
| Kill Window | Destroys a window on your screen without saving any changes. |

Window managers not only control the layering of windows on your desktop, they also maintain information about window positions, the look and feel of the windows, the condition of the window, and the expression of all of the interface elements that windows contain: borders, title bars, scroll bars, and so forth. The operations you perform on windows—open a window, close a window, resize a window, move a window, and so on—are commands issued to the Window Manager’s API (application programming interface). In Solaris, the Window Manager also stores session information that preserves the state of application windows and desktop conditions from one login of a user to the next.