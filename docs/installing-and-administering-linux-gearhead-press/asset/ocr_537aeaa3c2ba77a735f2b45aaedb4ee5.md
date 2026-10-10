# Table 14.4 Selected xterm Options

| OPTION | EXPLANATION |
|---|---|
| -bg color | Background color of the window |
| -cr color | Cursor color. The default color is the foreground color. |
| -display Name:Number | Host server name and X server display number where the command will run. If not specified, the client program gets the hostname and displays the number from the DISPLAY environment variable. |
| -e command | Command to be executed in the window. This flag executes a command; it does not start a shell. The command and its arguments (if any) must appear last on the xterm command line. |
| -fg color | Foreground color of the window |
| -fn font | Font to be used for all normal-sized text |
| -fullcursor | Full height (not the underscore style) text cursor |
| -geometry | Geometry location and dimensions of the window. The default is 80x25+0+0; that is, 80 pixels wide, 25 pixels long, located in the top-left corner (that is, at the 0,0 position) of the screen. |
| -help | Available option flags |
| -i | Display a newly created window as an icon, not a window. |
| -keywords | List the Xdefaults keywords. |
| -l | Append output from the xterm command to the login. |
| -lf file | The location where the output is saved. The default file is xterm.logxxxx, where xxxx is the PID of the xterm command. |
| -n icon name | Icon name used by the xterm command |
| -name application | The application name to use for Xdefaults |
| -sb | Scrollbar. -leftbar places the scrollbar on the left. |
| -sl | Maximum number of lines to save that are scrolled off the top of a window. The default is 64. |
| -T title | Name of the window in the title bar. If -n is not specified or a name for the icon has not been specified in .Xdefaults, this name is displayed also on the icon of the window. |
| -W | Move the cursor to the middle of the xterm window when it is created. |
| -xrm string | Resource string to be used |