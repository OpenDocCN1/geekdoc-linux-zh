# Advanced Bash-Scripting Guide

```
# -v: verbose

OPTS=-rtv --delete-exclude --delete-after --partial"

# rsync include pattern
# Leading slash causes absolute path match.
INCLUDE=(
  "/4/i386/kde-i18n-Chinese*"
  \^
  # Quoting is necessary to prevent globbing.
)

# rsync exclude pattern
# Temporarily comment out unwanted pkgs using "#" . .
EXCLUDE={
  /1
  /2
  /3
  /testing
  /4/SRPMS
  /4/Pec
  /4/i386_64
  /4/i386/debug
  "/4/i386/kde-i18n-*"
  "/4/i386/openoffice.org-lang-pack-*"
  "/4/i386/*.rpm"
  "/4/i386/GFS-*"
  "/4/i386/cman-*"
  "/4/i386/dlm-*"
  "/4/i386/gnbd-d-*"
  # "/4/i386/kernel-smp-*"
  # "/4/i386/kernel-xen-*"
#  "/4/i386/kernel-xen-*"
}
```

```
init () {
  # Let pipe command return possible rsync error, e.g., stalled network.
  set -o pipefail # Newly introduced in Bash, version 3.

TMP=$(${TMPDIR:-/tmp}/($#)).$S # Store refined download list.
trap '
  rm -f $TMP 2>/dev/null
  ' EXIT # Clear temporary file on exit.
}
```

```
check_pid () {
  # Check if process exists.
  if [ -s "SPID_FILE" ]; then
    echo "SPID file exists. Checking..."
    PID=$(/bin/grep -E "[:digit:]+" $SPID_FILE)
    if /bin/ps -p $SPID 2>/dev/null; then
      echo "SPID found. ($#) seems to be running!"
      /usr/bin/logger -t $($#) seems to be running!"
    else
      echo "SPID found. ($#) seems to be running!"
    fi
    exit $SE_RETURN
  fi

  echo "Process SPID not found. Start new process .."
}
```

Chapter 16. External Filters, Programs, and Commands

285