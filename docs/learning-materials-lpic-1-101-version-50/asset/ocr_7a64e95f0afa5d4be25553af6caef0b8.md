First we type Ctrl + a-. Then we use the arrow keys to mark the one that says 0 bash and press enter. Finally, we type Ctrl + a-A, type in top and press enter.

+   Check that the names have changed by having the window names displayed at the bottom of the screen again:

Ctrl + a-w

+   Now, detach the session and have screen create a new one named ssh:

Ctrl + a-d screen -S "ssh" and press enter.

+   Detach also from ssh and have screen display the list of sessions:

Ctrl + a-d screen -list or screen -ls.

+   Now, attach to the first session using using its PID:

screen -r PID-OF-SESSION

+   You should be back at the window displaying top. Split the window horizontally and move to the new empty region:

Ctrl + a-S

Ctrl + a-Tab

+   Have screen list all windows and select vi to be displayed in the new empty region:

We use Ctrl + a- to have all windows displayed for selection, mark vi and press enter.

+   Now, split the current region vertically, move into the newly created empty region and associate it with a brand new window:

Ctrl + a-|

Ctrl + a-Tab

Ctrl + a-c

+   Terminate all regions except the current one (remember, although you kill the regions, the windows are still alive). Then, quit out of all the windows of the current session until the session itself is terminated:

Ctrl + a-q. exit (to exit Bash), Shift + ~, then we type quit and press enter (to exit vi). After that,