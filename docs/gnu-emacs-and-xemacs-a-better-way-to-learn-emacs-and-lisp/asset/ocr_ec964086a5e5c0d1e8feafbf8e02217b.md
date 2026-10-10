![](bbox=[0.19, 0.08, 0.81, 0.42])

Figure 15.2 A Partially Folded Buffer

# Keyboard and Menu Commands

The default prefix for Folding mode commands is Ctrl-c @, a prefix I refuse to use. Casting about for a superfluous Emacs keybinding to co-opt as a prefix for Folding mode, I happened across Ctrl-v. The default binding runs the scroll-up command, which also happens to be the command called by the Page Up key. Since I never use Ctrl-v, preferring single keystrokes when possible, Ctrl-v seemed like a good candidate. If you like to do the same, you first need to unset the current binding with this line in your \~/.emacs file:

```
```elisp
(define-key global-map [(control v)] nil)
```
```

This line needs to be earlier in the \~/.emacs file than your Folding mode initialization lines. Now you are free to assign a new meaning to the Ctrl-v prefix. This can be done with Customize. Bring up the Folding Group Customize buffer by pressing M-x and typing

customize-group

When prompted, type

folding

Several folding settings can be changed in the resultant Customize buffer. The default prefix key is the first setting.