# DESCRIPTION

See a part of a context. The context is taken from a file, pid, user input or the context in which **secon** is originally executed.

+   - -V, **—version**
+       shows the current version of secon
+   - -h, **—help**
+       shows the usage information for secon
+   - -P, **—prompt**
+       outputs data in a format suitable for a prompt
+   - -C, **—color**
+       outputs data with the associated ANSI color codes (requires -P)
+   - -u, **—user**
+       show the user of the security context
+   - -r, **—role**
+       show the role of the security context
+   - -t, **—type**
+       show the type of the security context
+   - -s, **—sensitivity**
+       show the sensitivity level of the security context
+   - -c, **—clearance**
+       show the clearance level of the security context
+   - -m, **-s-range**
+       show the sensitivity level and clearance, as a range, of the security context
+   - -R, **—raw**
+       outputs the sensitivity level and clearance in an untranslated format.
+   - -f, **—file**
+       gets the context from the specified file FILE
+   - -L, **—link**
+       gets the context from the specified file FILE (doesn't follow syinks)
+   - -p, **—pid**
+       gets the context from the specified process PID
+   - **—pid-exec**
+       gets the exec context from the specified process PID
+   - **—pid-fs**
+       gets the fscrate context from the specified process PID
+   - **—current**, **—self**
+       gets the context from the current process
+   - **—current-exec**, **—self-exec**
+       gets the exec context from the current process
+   - **—current-fs**, **—self-fs**
+       gets the fscrate context from the current process
+   - **—parent**