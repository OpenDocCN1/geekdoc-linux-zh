The ease with which HTML support is added to the text widget may you think that it would be easy to write a full browser with Tk. Before you do too much work on that project, take a look at Steve Ball's plume browser at http://tcltk.anu.edu.au/1.0al/ and read Mike Doyle and Hattie Schroeder's book Web Applications in Tcl/Tk. Much of the work that you'll need to create a browser has already been done.

# 10.5 Bottom Line

+   - The text widget can be used to display formatted text.
- The text widget can be configured to allow the user to edit the text.
- The text widget supports:
  - Multiple fonts
  - Multiple colors for foreground and background
  - Varying margins
  - Varying line spacing
  - Binding actions to characters or strings
  - Including images and other Tk widgets in the text
- Locations in the text widget are identified as line and character positions. Only locations where text exists can be accessed.
- Lines that are longer than the display can wrap. If this occurs, then the line and character index points reflect the internal representation of data, not the display.
- A text widget is created with the text command.
  Syntax: textName ?options?
- Text is inserted into a text widget with the insert subcommand.
  Syntax: textName insert index ?tagList? \ ?moreText? ?moreTagList? ...
- An image is inserted into a text widget with the textName image create subcommand.
  Syntax: textName image create index ?options?