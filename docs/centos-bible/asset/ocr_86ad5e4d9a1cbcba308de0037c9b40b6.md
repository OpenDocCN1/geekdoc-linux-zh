# **TABLE 3-1**

# Metacity Keyboard Shortcuts

| Actions | Keystrokes |
| :--- | :--- |
| **Window focus** | |
| Cycle forward, with pop-up icons | [Alt]+[Tab] |
| Cycle backward, with pop-up icons | [Alt]+[Shift]+[Tab] |
| Cycle forward, without pop-up icons | [Alt]+[Esc] |
| Cycle backward, without pop-up icons | [Alt]+[Shift]+[Esc] |
| **Panel focus** | |
| Cycle forward among panels | [Alt]+[Ctrl]+[Tab] |
| Cycle backward among panels | [Alt]+[Ctrl]+[Shift]+[Tab] |
| **Workspace focus** | |
| Move to workspace to the right | [Ctrl]+[Alt]+right arrow |
| Move to workspace to the left | [Ctrl]+[Alt]+left arrow |
| Move to upper workspace | [Ctrl]+[Alt]+up arrow |
| Move to lower workspace | [Ctrl]+[Alt]+down arrow |
| Minimize/unminimize all windows | [Ctrl]+[Alt]+D |
| Show window menu | [Alt]+spacebar |
| Close menu | [Esc] |

+   - **Move Windows to Other Workspaces** — Click on any window, each represented by a tiny rectangle in the Workspace Switcher, to drag-and-drop it to another workspace. Likewise, you can drag an application from the Window List to move that application to another workspace.
+   - **Add More Workspaces** — Right-click on the Workspace Switcher and select Preferences. You can add workspaces (up to 32).
+   - **Name Workspaces** — Right-click on the Workspace Switcher and select Preferences. Click in the Workspaces pane to change names of workspaces to any names you choose.

You can view and change information about Metacity controls and settings using the `gconf-editor` window (as root, type `yum install gconf-editor` and then `gconf-editor` as a regular user from a Terminal window). As the window says, it is not the recommended way of changing preferences. So, when possible, you should change the desktop through GNOME preferences. However, `gconf-editor` is a good way to see descriptions of each Metacity feature.