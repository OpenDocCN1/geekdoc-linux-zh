vi editor commands (such as x to delete a character and i to insert text). Once you are finished editing the command line, you must press the Esc key again to exit vi editor mode.

# The Dash environment variables

There are quite a few default environment variables that the Dash shell uses to track information, and you can create your own environment variables as well. This section describes the environment variables and how Dash handles them.

# Default environment variables

The Dash environment variables are very similar to the environment variables used in Bash (see [Chapter 5](#chapter-5), “Understanding the Shell”). This is not by accident. Remember that both the Dash and Bash shells are extensions of the Bourne shell, so they both incorporate many of its features. However, because of its goal of simplicity, the Dash shell contains significantly fewer environment variables than Bash. You need to take this fact into consideration when creating shell scripts in a Dash shell environment.

The Dash shell uses the set command to display environment variables:

```
$set
COLORTERM=''
DESKTOP_SESSION='default'
DISPLAY=':0.0'
DM_CONTROL='/var/run/xdmctl'
GS_LIB='/home/atest/.fonts'
HOME='/home/atest'
IFS=''
'
KDEROOTHOME='/root/.kde'
KDE_FULL_SESSION='true'
KDE_MULTIHEAD='false'
KONSOLE_DCOOP='DCOPRef(konsole-5293,konsole)'
KONSOLE_DCOOP_SESSION='DCOPRef(konsole-5293,session-1)'
LANG='en_US'
LANGUAGE='en'
LC_ALL='en_US'
LOGNAME='atest'
```