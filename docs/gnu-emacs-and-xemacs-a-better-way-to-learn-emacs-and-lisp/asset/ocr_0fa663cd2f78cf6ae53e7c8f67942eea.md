# # Outline Mode

Outline mode is used when you’re writing structured documents that have a predictable hierarchy. Any document that is divided into sections is suitable for this mode. Outline mode allows you to “collapse” a buffer so that only the section titles or headers are visible. Figure 14.13 shows the same document in both windows. The upper window is the normal expanded view, and the lower window has been collapsed with the command Hide Leaves from the Hide menu.

Outline mode uses a tree analogy when referring to the various parts of a document: the “leaves” are the actual text content under a heading or subheading. A parent-child analogy is also used, with the content under a heading (including subheadings and their content) thought of as the children of a parent heading.

# ## Starting Outline Mode

You can turn on Outline mode by pressing M-x and typing

```
outline-mode
```

This makes Outline mode the major mode. Outline mode is designed to work in conjunction with text-mode, so your text-mode settings will still be in effect.

Outline mode doesn’t have to be a major mode. You might want to use it along with another mode, such as one of the programming-language modes. Outline minor mode is really the same mode, but the keybindings are different so that it

![](bbox=[0.19, 0.63, 0.83, 0.95])

Figure 14.13 Buffers in Outline Mode