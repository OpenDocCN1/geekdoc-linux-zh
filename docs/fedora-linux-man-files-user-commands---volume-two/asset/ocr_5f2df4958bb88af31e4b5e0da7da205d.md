# > ARGUMENTS

+   username

The username for the user for which you want to query or modify the fingerprint database.

Not that **fprintd-list** and **fprintd-delete** require at least one username to be passed, and support multiple usernames.

**fprintd-enroll** and **fprintd-verify** will use the current username if none are passed on the command-line.

+   -f finger

For **fprintd-enroll**, the finger to enroll. Possible values are:

left-thumb, left-index-finger, left-middle-finger, left-ring-finger, left-little-finger, right-thumb, right-index-finger, right-middle-finger, right-ring-finger, right-little-finger.

The default is automatic, selecting the first available finger for swipe devices, or all the enrolled fingers, for press devices.