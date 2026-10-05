The internal key numbers used in text mode (for loadkeys and shawdey) and under X (for xmodmap and xev) do not correspond! In text mode, the Backspace key is number 14, under X 22.

For more advanced X programs, this instruction is sufficient and BackSpace works satisfactorily. Other programs will not know what to do with BackSpace and continue interpreting the Delete string as BackSpace. With such programs, a modification in ~/.Xdefaults or ~/.Resources sometimes wonders (see also page 248).

# Keys in text mode programs

Even under X, you will often find yourself working with programs that were designed to be used in text mode (jed, pine, and so on). For such programs, the above instruction is of little use. The weirdest comes on the effect of the jed editor: Backspace calls the online help, and Del
Under X, text mode programs are executed in a terminal or shell created by the xterm. This allows you to achieve correct support for nearly all traditional programs with a single change in the xterm resources. Simply insert the following lines into ~/.Xdefaults or ~/.Resources file depending on the distribution:

```
! in ~/.Xdefaults or ~/.Resources
VT100.Translations: override |
<Key>+Backspace: string(0x7f)\\n<Key>+Delete: string(0x04)

<Key>+Home: string(0x01)

<Key>+End: string(0x05)
```

This setting refers to the VT100 window which is, however, the bezier of a line. The Keystring string Backspace is substituted with character code 127 and the Keystring string Delete with character code 4 (this corresponds to Ctrl+D). Following the same pattern, Home can be assigned to Ctrl+A and End to Ctrl+E, so that these keys can be used, as in text, to jump to the beginning or the end of a line.

Thus, the four keys are interpreted correctly by a large number of programs. These settings have also been tested with Emacs in text mode (emacs -nw), with jed, jose, bash, and so on.

In order to force the X version of Emacs to recognize Backspace and Del, you must include the following line in ~/.emacs:

```
; in ~/.emacs
(global-set-key [delete] delete-char) ;<Del> delete character
```