# Advanced Bash-Scripting Guide

# In 1978, Leo Christopherson wrote an animated version of Nim,
## Android Nim, for the TRS-80 Model I.

# Example A-43. A command-line stopwatch

```
#!/bin/sh
# sw.sh
# A command-line stopwatch

# Author: Pádrig Brady
# http://www.pixelbeat.org/scripts/sw
# (Minor reformatting by ABS author.)
# Used in ABS Guide with script author's permission.
# Notes:
# This script starts a few processes per lap, in addition to
# the shell loop, so the assumption is made that
# this takes an insignificant amount of time compared to
# the response time of humans (~1) (or the keyboard
# interrupt rate (~ms))
# ? for split must be entered twice if characters
# (erroneously) entered before it (on the same line).
# ? since not generating a signal may be slightly delayed
# on loaded systems.
# Lap timings may be delayed due to:
# https://bugs.launchpad.net/bugs/62511
# Changes:
V1.0, 23 Aug 2005, Initial release
V1.1, 26 Aug 2007, Allow split and laps from single invocation.
Only start timer after a key is pressed.
Indicator lap number
Cache programs at startup so there is less error
due to startup delays.
V1.2, 01 Aug 2007, Work around 'date' commands that don't have
nanosecond precision.
# Use stty to change interrupt keys to space for
laps etc.
# Ignore other input as it causes problems.
V1.3, 01 Aug 2007, Testing release
V1.4, 02 Aug 2007, Tweaks to get working under ubuntu
and Mac OS X.
V1.5, 27 Jun 2007, set LANG=C as got vague bug report about it.
```

```
export LANG=C

imit -c 0 # No core dumps for SIGQUIT.
trap '' TTSTP # Ignore Ctrl-Z just in case.
stave_tty -g -# trap "stty save_tty" EXIT # Restore tty on exit.
stty quit "?" # Space for laps rather than Ctrl-\.
stty eof '?' # ? for splits rather than Ctrl-D.
stty -echo # Don't echo input.

cache_progs() {
nstty > /dev/null
date > /dev/null
grep < /dev/null
(echo "import time" | python) 2> /dev/null
bc < /dev/null
sed '' < /dev/null
printf '1' > /dev/null
/usr/bin/time false 2> /dev/null
}
```

Appendix A. Contributed Scripts

727