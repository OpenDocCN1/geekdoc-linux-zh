![](bbox=[0.1, 0.09, 0.93, 0.16])

Figure 2.6: Nginx fails to restart due to a missing include file

![](bbox=[0.1, 0.25, 0.93, 0.32])

Figure 2.7: The syntax test of the configuration file has completed successfully

# 2.4 Base modules

The base modules allow us to define the basic parameters and configuration of Nginx. They are built-in into Nginx automatically during compile time. Their directives and blocks are always available. There are three types of base modules:

+   The core module contains essential directives and features. Most of its directives must be placed at the root (meaning the top) of the configuration file and are only used once. Table 1 shows some directives in the core module with a brief explanation and context (if no context is specified, the actual context is global and the directive must be placed at the root of the configuration file).

Table 2.1: Some Events Module directives

| Directive/Context | Syntax and description |
|---|---|
| `daemon` | Accepted values: on / off Syntax: daemon on; Enables or disables daemon mode (starts the program in the background or the foreground, respectively). Useful to troubleshoot issues. |
| `env` | Syntax: env MY_VARIABLE=my_value; Allows us to define or define environment variables. |
| `error_log` | Context: `main`, `http`, `server`, and `location`<br>Syntax: error_log /path/to/file level (where level can be one of the following values: debug, info, notice, warn, error, and crit, depending on the type of errors that we want to save in the log file). To disable error logging, redirect the log output to /dev/null: error_log /dev/null crit; |
| `master_process` | Accepted values: on / off Default value: on If enabled (on) Nginx will start both the master process and worker processes. If disabled, Nginx will work with a unique process. This is used for debugging purposes only and will cause that clients won’t be able to connect to the server. |
| `pid` | Syntax: file path Default value: defined at compile time. Path of the file where the PID of Nginx will be stored. |