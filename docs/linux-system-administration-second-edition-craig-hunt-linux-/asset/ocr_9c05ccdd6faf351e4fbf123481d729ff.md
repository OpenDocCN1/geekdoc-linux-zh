This procedure is not without its drawbacks, unfortunately. Step 3 relies upon the presence of an SSH client on the X server and an SSH server on the X client. You could modify this command to use rsh rather than ssh, but rsh isn't a very secure protocol, so such a modification is inadvisable. This step extracts an authentication key that the X server uses to determine who may access it, and transfers that key to the X client system. It's possible to perform the task accomplished in step 3 by using the xauth utility in interactive mode and transferring the key manually, but doing so is a tedious process.

If you use SSH in step 4, SSH may attempt to tunnel X connections. In fact, as described earlier, in "Using xhost on the X Server," doing this obviates the need to perform the procedure described here, and in this isn't really a drawback of the use of xauth. If SSH is installed on both computers, it's generally preferable to use SSH's X tunneling capabilities, because this provides encryption. Without such encryption, all data passed as part of an X session are vulnerable to capture by miscreants.

Some X tools use xauth "behind the scenes." For instance, XDM and similar tools (described in the upcoming section, "Starting X Automatically") use xauth to grant users access to the X server. SSH does the same when it tunnels connections, although in this case X uses xauth locally and stands in for an X server on the X client system, and for the X client on the X server system.

# ## X Virtual Consoles

Chapter 6 described the use of virtual consoles for text-mode logins. If you use a text-mode login, you can hit Alt+F1 through Alt+F6 to switch between different screens, each of which can display a different login session. You can therefore use one to log in with your normal username, another to log in as root, and so on; or log in multiple times as one user and switch easily between different programs. If you're running X, you can switch to a virtual text-mode console by pressing Ctrl+Alt+Fn, where n is the console number.

Virtual consoles are not restricted to text-mode logins, however. When X runs, by default, it takes over an unused virtual console (typically console 7). You can therefore switch back to X from a text-mode console by pressing Alt+F7 (if X is running). Of potentially greater interest, it's possible to run multiple X sessions, each in its own virtual console. You can then switch between them by pressing Ctrl+Alt+Fn, where n is a number from 7 up. To launch a second X session, follow these steps:

+   1. If you're already running in X, press Ctrl+Alt+F1 to get to a text-mode login: prompt. Log in.   
2. Type `startx -- :1 vt8` to start X on virtual terminal 8. You should see X start up.   
3. Press Ctrl+Alt+F7 to switch back to your original X session or Ctrl+Alt+F8 to switch to the new one.

Why would you want to start a new X session? After all, most window managers support multiple workspaces, so you can easily keep lots of windows open on different screens. You can even use su within an xterm to launch programs as different users. Using multiple X sessions does have certain advantages, however:

+   - You can run different window managers in different sessions. This isn't ordinarily a compelling reason to run multiple sessions, but it can be useful if you want to evaluate a window manager or if you need to use one for some programs but prefer another for other programs.
- You can start X in different resolutions. Your normal startup might be in 1280×1024 resolution, but if you need to test software at 800×600, you can run a separate 800×600