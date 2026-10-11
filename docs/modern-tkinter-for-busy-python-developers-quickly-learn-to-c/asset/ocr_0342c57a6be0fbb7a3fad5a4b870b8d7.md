# Conventions

As is typically done, code listings, interpreter or shell commands and responses will be indicated with a fixed-width font. When showing an interactive session with the interpreter, the parts that you enter will additionally be in **bold fixed-width**.

When describing procedure or method calls, the literal parts (e.g. the method name) will be in plain fixed-width font, parameters where you should fill in the actual value will add *italics*, and optional parameters will be surrounded by “?”, e.g. “set variable ?value?”.

A number of icons appearing to the left of text are used, as follows:

This paragrah consists of material that is specific to the Python binding to Tk.

This paragraph will help point out common mistakes that people make, or suggest useful but not necessarily obvious solutions related to the topic.

This indicates a new way of doing things in Tk 8.5 that is very different from the way things would have been done previously. People familiar with older versions of Tk, or working on programs developed with older versions of Tk, should pay close attention.

This paragrah provides some additional background information, not strictly necessary to understanding the topic at hand, but that might help you understand a bit more about how or why things are done the way they are.

This indicates some error in the tutorial itself which hasn’t yet been corrected, or a section that has been deleted but not yet replaced.

This indicates an area in Tk that could most charitably be described as a “rough edge”. It may indicate a bad or missing API requiring you to use a workaround in your code. Because these things tend to get fixed up over time, it’s worth marking them in your code with a “TODO” so you can remember to go back later and see if a newer API resolves the problem cleanly.

# Installing Tk

In this chapter, you’ll get Tk installed on your machine, verify it works, and then see a quick example of what a Tk program looks like.

Though pretty much all Mac OS X and Linux machines come with Tk installed already, it’s usually an older version (typically 8.4.x). You want to make sure you’ve got at least version 8.5 to use the new widget set, so if that’s not already there, you’ll want to install the newer version.

Though there are lots of ways to install Tk, the easiest is to download and install one of the versions provided by ActiveState (www.activestate.com).

ActiveState is a company that sells professional developer tools for dynamic languages. They also provide (for free) quality-controlled distributions of some of these languages, and happen to employ a number of core developers of these languages.