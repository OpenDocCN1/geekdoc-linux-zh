# An Overview of the emacs Editor

Finally, using C-x u three times causes the original text to be restored:

> A Tale of Two Cities
Preface

When I was acting, with my children and friends, in Mr Wilkie Collins’s drama of The Frozen Deep, I first conceived the main idea of this story. A strong desire came upon me, then, and I traced out in my fancy, the state of mind of which it would necessitate the presentation to an observant spectator, with care and interest.

As the idea became familiar to me, it gradually shaped itself into its present form. Through its execution, it had complete possession of me; I have so far verified what is done and suffered in these pages, as that have certainly done and suffered all myself.

Whenever any reference (however slight) is made here to the condition of the French people before or during the Revolution, it is truly made, on the faith of the most trustworthy witnesses. It has been one of my hopes to add
------Emacs: dickens.note (Fundamental)------Undo!

If you don't have a Delete key, some of the deletion commands will be unavailable to you, regrettably. Generally, though emacs has as many ways to delete text as vi, if not more. The best feature, is that, unlike vi, emacs remembers edit changes from the beginning of your editing session. You can always back up as far as you want by using the C-x u undo.

The deletion command keys are summarized in Table 13.2.

# Table 13.2. Deletion commands in emacs.

| Command | Meaning |
| Delete | Delete the previous character. |
| C-d | Delete the current character. |
| M-Delete | Delete the previous word. |
| M-d | Delete the next word. |
| C-x Delete | Delete the previous sentence. |
| M-k | Delete the rest of the current sentence. |
| C-k | Delete the rest of the current line. |
| C-x u | Undo the last edit change. |