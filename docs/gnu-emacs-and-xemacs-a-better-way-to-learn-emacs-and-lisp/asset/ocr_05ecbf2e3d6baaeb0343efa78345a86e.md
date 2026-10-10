X Window was several years ago, when I discovered that font servers for TrueType fonts were available.

TrueType fonts were developed in the late '80s by Apple as part of an agreement with Microsoft. The motivation of the two companies was to counter the impending dominance of Adobe's font technology in the emerging personal computer market. Apple's new fonts were designed to look clear and sharp on a computer monitor. Naturally, the Microsoft-Apple alliance hoped that the new style of fonts would supplant Adobe's rival PostScript Type 1 font standard. This didn't happen. PostScript fonts are still the norm in the publishing industry, but for on-screen display, TrueType fonts are exceptional.

The 4.0x releases from the XFree86 Project are a milestone for the Linux user. The major Linux distributions are making the transition from the old 3.3x releases. Because of this, the installation and use of TrueType fonts has become easier. The new XFree86 releases come with built-in support for TrueType fonts. The xf86font server can make them available to applications, a job that previously required the services of a third-party font server.

After you have installed some good-quality TrueType fonts, they will show up in the Font section of the XEmacs Options menu.

# ## Your Own Keybindings

Only so many keystroke combinations are available on a standard keyboard. The Emacs developers tried to assign keystrokes to the most commonly-used commands while making other commands available as M-x minibuffer commands. There's a good chance that you don't entirely agree with their decisions. Some keybindings might feel awkward, while others that you use constantly deserve to be elevated from multikeystroke to single-keystroke bindings.

This is an area where the sheer configurability of Emacs shines. After you learn to use some fairly simple Lisp functions, any or all keys can be rebound to other keystrokes.

One note of caution: If you go hog-wild with massive keybinding changes, using another Emacs configured "normally" could be a painful experience. If you work in a corporate environment and you occasionally need to use Emacs on other users' machines, it might be wise to keep at least the basic key commands on your machine close to the default. This is one reason why the supposedly more-efficient Dvorak keyboard layout isn't used more widely: A Dvorak user at a QWERTY keyboard can be reduced to the hunt-and-peck style of typing.