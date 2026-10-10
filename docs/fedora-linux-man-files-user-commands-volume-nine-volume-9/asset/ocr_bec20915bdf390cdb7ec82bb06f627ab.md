+   -p `dl-search-path` = PATH
+   
+   Set the search path for dynamic shared objects (plugins).

+   — **resample-thod** = METHOD
+   
+   Use the specified resampler by default (See **—dump-resample-thods** above for possible values).

+   — **use-pid-file** [=BOOL]
+   
+   Create a PID file. If this options is disabled it is possible to run multiple sound servers per user.

+   — **no-cpu-limit** [=BOOL]
+   
+   Do not install CPU load limiter on platforms that support it. By default, PulseAudio will terminate itself when it notices that it takes up too ch CPU ti. This is useful as a protection against system lockups when real-ti scheduling is used (see below). Disabling this chanism is useful when debugging PulseAudio with tools like **{1}** which slow down execution.

+   — **disable-shm** [=BOOL]
+   
+   PulseAudio clients and the server can exchange audio data via POSIX shared mor y segnts (on systems that support this). If disabled PulseAudio will communicate exclusively over sockets. Please note that data transfer via shared mor y segnts is always disabled when PulseAudio is running with **—system** enabled (see above).

+   -L `load` ="MODULE ARGUMENTS"
+   
+   Load the specified plugin module with the specified argsmts.

+   -F `file` =FILENAME
+   
+   Run the specified script on startup. May be specified multiple tis to specify multiple scripts to be run in order. Coine with **-n** to disable loading of the default script default.pa (see below).

+   -C
+   
+   Open a command interpreter on STDIN/STDOUT after startup. This may be used to configure PulseAudio dynamically during runti. Equivalent to `load=module-cli`.

+   -n
+   
+   Don't load default script file default.pa (see below) on startup. Useful in conjunction with **-C** or **—file**.