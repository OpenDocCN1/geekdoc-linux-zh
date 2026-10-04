# 10.4 HTML Display Package

```
}
############################################################
# proc HMlink_callback {win href}--
# This proc is called by the html_library code to parse a
#    hypertext reference.
#
# Arguments
# win      The text window that is used by the html_library to
          display the text
# href     A hypertext reference to use for the next hyper-
          text.
#
# Results
# This example simply replaces the contents of the display
# with hardcoded new text.

proc HMlink_callback {win href} {
    global newHTMLTtxt

    puts "HMlink_callback was invoked with WIN: $win HREF: \
$shref"

    # Clear the old contents from the window.
    HMreset_win $win

    # Display the new text.
    HMparse_html $newHTMLTtxt "HMrender $win"
}

############################################################
# proc HMset_image {win handle src}--
# Acquire image data, create a Tcl image object,
# and return the image handle.
#
# Arguments
# win      The text window in which the html is rendered.
#        handle   A handle to return to the html library with the
#               image handle
# src      The description of the image from: <IMG src=XX>>
```

381