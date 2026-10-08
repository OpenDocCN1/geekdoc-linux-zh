sider it a CDE working file and forget about it. The **.Xdefaults** file is where you or an end user would list X resources specific to the user's personal CDE environment. **sys.resources**, **dt.resources**, and **Xdefaults** contain a list of resources and their values.

The **sys.sessions** file controls which clients start the very first time a new user logs into CDE. The **dt.sessions** file is to **sys.sessions** as **dt.resources** is to **sys.resources**.

It may be efficient to configure CDE to start particular applications for your users. You would specify these applications in **sys.sessions**. When a new user logs in for the first time, the CDE environment includes the specified clients. At the end of the first session by logging out, the remaining clients would be recorded in **SHOME/.dt/sessions/current** for CDE (SHOME/.dt/sessions/home when the home session is restored).

The **sys.dtprofile** file is a template that is automatically copied at first login into each new user's home directory as **.dtprofile**. **sys.dtprofile** replaces **.profile** or **.login** in the CDE environment (although either **.profile** or **.login** can be sourced in **.dtprofile** by removing the # comment symbol in front of **DTSOURCEPROFILE=true**). The **.dtprofile** file holds the personal environment variables that would, in a character-based environment, be found in **.profile** or **.login**. Use **.dtprofile** to avoid the interference that terminal I/O commands cause to CDE's graphical environment.

The CDE login manager, **dlogin**, presets the following environment variables to default values:

+   - **DISPLAY** The name of the local display
- **EDITOR** The default text editor
- **HOME** The user's home directory as specified in /etc/passwd
- **KBD_LANG** The current language of the keyboard
- **LANG** The current NLS language
- **LC_ALL** The value of LANG
- **LC_MESSAGES** The value of LANG
- **LOGNAME** The user's login name as specified in /etc/passwd
- **MAIL** The default file for mail (usually /var/mail/USER)