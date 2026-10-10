# **Debug Mode**

In our deployment examples, we made a decision to turn debugging off. A change can be made in your `/etc/puppet/hiera/common.yaml` file in order to adjust debug level for each service and then you run the appropriate `puppet apply` command for that deployment scenario. Having debugging enabled is rarely the default because it produces a considerable number of logs that are unnecessary when a deployment is functioning normally. If you’re not using Puppet in your production deployment, you will want to refer to the documentation for each service to learn how to turn on debugging, but it will typically look something like this:

```
```
debug=True
```
```

As with any modification to a configuration file, we recommend that you make a backup of the configuration file you began with, even if you’re using a configuration management system. Having a starting point can help when you forget where you began or are seeking to pass off debugging to another engineer. You will then need to restart the respective service or services that are logging to that file for the debug change to take effect.

# **Tip**

There are cases when debugging is left on for particular services for auditing or long-term debugging. Be aware of the problem spots in your infrastructure so you can make informed decisions about whether a service should run with debugging on long term or not.

# **Understanding Log Messages**

There are two main things you should keep in mind about OpenStack when reading log messages:

+   * It is written in Python, so you may encounter a lot of Python tracebacks, which provide stack trace information. As such, standard Python documentation on reading errors can be useful if the errors are not obvious to you.

+   * OpenStack is modular—it depends on various different components. When you see an error in one service, it may actually be due to a problem in another. We’ll dive into specifics of the likely candidates in the “Key Services” section of this chapter.

When debugging systems which are written in Python, a good general strategy is to first look at the last line in the traceback. This may give you a clear indicator of what went wrong. If the last line is not helpful, go to the top of the traceback and read through it for anything obvious.

If you don’t find anything in the traceback itself just yet, look at the lines in the log file above it. If you have debug enabled, you may need to sift through some lines to find actual errors. A command that a service depends on may be failing to complete successfully, you may have an authentication problem or perhaps there is an error about running out of resources, like memory. Once you find the error, having the debug lines