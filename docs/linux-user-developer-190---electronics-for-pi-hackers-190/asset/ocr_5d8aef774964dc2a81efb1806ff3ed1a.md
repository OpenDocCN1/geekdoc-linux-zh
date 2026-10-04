# Review

# Interactive Shells

# In brief: compare and contrast our verdicts

| Installation | bpython | DreamPie | IPython | ptpython |
| --- | --- | --- | --- | --- |
| Available in distribution repos as well as in the Python Package Index | Clone its git repo or install using your distro's repositories or Python's hippie | Recommends that you use pip, but is also available in distribution repositories | Not available in the repositories and can only be installed via pip package manager |
| features | Autocomplete, highly syntax, rewind and can also save session to Pastion | Can detect much more and save an extra entry in external file for keys | Trumps the others in sheer number of features and functionality | Has all the intuitive interactions along with emacs and bindings |
| Usability | Can be used right after installation, application help and supports customisation | The Shell offers a unique two-pane display with intuitive menu layout | Users need to refer to documentation to make full use of it | Quite useful for non-helpful suggestions |
| Help and support | Offers inbrief help and has a section on its own website | Has a detailed guide how to use and books to its name | Lacks a decent set of terms for a user reader |
| Overall | Offers enough for both new and experienced coders | There's an interesting code from the output, but it is not actively updated | Despite its, Python is much better than just another interactive shell | Will make sense to experienced keyboarders than new coders |

# AND THE WINNER IS ...

# bpython

The main idea behind interactive shell is to shake away the vanilla Python interpreter that makes coding on the command line easier. It would be good to consider this as a replacement for an IDE; however, a good interactive shell will be better than an IDE for a lot of tasks.

We don't recommend DreamPie as it hasn't been updated in quite a while. Although it requires Python 2, you can run it; this worked for on Ubuntu 17 but not on Fedora 2. In terms of features, there's no beating it and overkill for an interactive shell.

Then there is which will be useful to experienced beginners. Along with all its features, bpython has the advantage of replacing Python, which enables you to use interesting features such as 'magic' functions. What we really like in Python is the history browser

While this is missing from our favourite interactive Shell, bpython,

![](bbox=[0.355, 0.575, 0.932, 0.715])

```
python
>>> bpython
>>> 17.1 on top of Python 3.6 /usr/bin/python3
>>> import math
>>> sqrt(x)
# Return the square root of x."
```

bpython has features of its own; if it sees something it doesn't understand it passes to Python

Its Ctrl-R review feature is pretty nifty as well. It is like-context-aware auto-completion that finds lots of options as you use. If you type type- an attribute, I'll install the module that you are working with and give you the relevant list of names. It is worth noting the discovery for modules is a wonderful help for learners.

We appreciate the ability to save sessions and file to Pasteln, bpython doesn't require any configuration so you get started immediately. You can modify the default configuration later to better suit your workflow.

Mayank Sharma

![](bbox=[0.068, 0.915, 0.335, 0.985])