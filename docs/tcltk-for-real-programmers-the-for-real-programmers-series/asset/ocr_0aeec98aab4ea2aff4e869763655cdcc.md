# Chapter 10. The text Widget and html_library

Script Output
HMset_image was invoked with WIN: .t HANDLE: .t7 SRC: logo
Script Results

![](bbox=[0.325, 0.203, 0.783, 0.273])

The html_library uses a technique similar to the image callback procedures to resolve hypertext links. When a user clicks on a hypertext link, a user-supplied procedure named HMlink_callback is invoked with the name of the text window and the contents of the href=value field.

Syntax: HMlink_callback win href

HMlink_callback
A procedure that is called from the html_library package when a user clicks on an <A href=value> field.

win
The text widget in which the new text can be rendered.
href
The hypertext reference.

The next example shows HMlink_callback that will display the HTML text contained in a Tcl variable. In a browser application, the HMlink_callback procedure would download the requested URL, and in a Help application it would load the requested help file.

Example 10.4.2-2

```
############################################################
# proc HMlink_callback (win href) --
# This procedure is invoked when a user selects a hypertext
# link in the HTML display.
#
 In an actual browser, the href field would contain the URL of
# the HTML page to retrieve. In this example, it contains the
# name of a Tcl variable.
```