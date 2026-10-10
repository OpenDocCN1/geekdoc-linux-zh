
## 13 Troubleshooting

> *Humpty Dumpty sat on a wall,*
> *Humpty Dumpty had a great fall.*
> *All the king’s horses and all the king’s men*
> *Couldn’t put Humpty together again.*
>
> *English nursery rhyme*

As we have learned, OpenStack is a complicated infrastructure project. Even if you followed the instructions in this book precisely and everything worked well, using OpenStack in production will not be the same. Troubleshooting your OpenStack deployment to find where failures are lurking is a vital skill.

Your toolbox for debugging may include sifting through log files or running specific commands manually. There are also services such as OpenStack’s Identity (Keystone) and Networking (Neutron) that can cause failures throughout your infrastructure if there is a configuration problem. We talk about debugging those.

### Reading Displayed Errors

Whether you’re using the dashboard or the command line, an error may manifest immediately, which may start pointing you in the right direction.

When looking for an error, the first step will be determining which service is the problem. Are you having trouble launching an instance? If you’re using the dashboard, your first indicator may be a pink box that pops up to tell you something is wrong. In Figure 13.1 it says “Error: Failed to perform requested operation on instance “zebra”, the instance has an error status: Please try again later [Error: No valid host was found. There are not enough hosts available.]”

By clicking on the name of the instance that failed, in this case “zebra”, you will see more details about the node itself. This will remind you of the settings you selected. It will also give you access to exposed log files and an Action Log that will show actions performed against the instance. The Console will not be available since that is only active when an instance is running. See Figure 13.2 for this detailed view.

![](img/8684900d708748f86bb043faa5589f9e_241_0.png)

Figure 13.1. Instance launch error in the Horizon dashboard

![](img/8684900d708748f86bb043faa5589f9e_241_1.png)

Figure 13.2. Instance details

If you have used the OpenStack Client (OSC) to create this instance, you would not get an immediate response, since the output only tells you that the instance is being created. Instead you may look at the listing of instances and then query that one specifically to read the error message. Note that we are using the ID of the instance to show details about the instance because the instance Name is not a unique identifier. You could have a whole herd of instances called zebra (Listing 13.1!)

As you can see, the listing showed that the instance was in an “ERROR” state. Full details will show you details from your instance, and “fault” will show the error message that is the same as what was shown in the dashboard.

Regardless of whether you’re viewing this output at the command line or in the dashboard, the first thing that can help you do is see whether you’ve made a mistake. Given this error, it’s easy to assume that the region you’re trying to launch it in really doesn’t have enough resources, but what if you’re sure it does? Did you perhaps launch it in the wrong region? Did you use the wrong image or flavor? These are easy to identify and easy to correct without going any further with troubleshooting.

More often than not, things are more complex. Using the error above as an example, you’ll want to keep in mind that it is given by a service that can only see part of the picture. A misconfiguration may signal to the service that the host does not satisfy the requirements, even if that host should be able to receive the instance request as specified. It does not necessarily mean that the service itself has a configuration problem.

To make matters worse, you may not even see an error message. You may discover that a block storage volume simply won’t attach to an instance or your network isn’t working as you expected it to.

These situations are when looking at the logs come in.

### Logs

In a production deployment of OpenStack, especially a large one, you will likely have a centralized logging system where all servers send logs to—maybe it’s even backed by the OpenStack Object Storage (Swift)! Having a centralized log system can also help with valuable older logs rotating out of existence, since saving logs of a functioning services to compare to your failures can be valuable. However, in this chapter we make the assumption that logs are being stored locally on each OpenStack node and will be referencing them accordingly.

After looking for obvious errors in your interface, log files will be your next stop in most troubleshooting scenarios. Logs for OpenStack services are typically found in /var/log/service-code-name, so you’ll find the logs for Compute (Nova) services in /var/log/nova.

> **Tip**
> Depending on the service and whether they contain sensitive data, such as hints about authentication, log files will vary in terms of permissions. You may need to use administrative access (using sudo) to view them.

### Listing 13.1

```
$ source net/openrc/test
$ openrc stack server list
```

| ID | Name | Status | Remarks |
|---|---|---|---|
| 4baf3781-bad8-4baf-86d5-3956f0cba88 | zebra | ERROR | |
| 4b7b729c-9de3-41b5-8691-d6ec3d5df74 | giraffe | ACTIVE | |
| aff723f3-94e8-a9e5-835f-4c9f83a0d8a8 | zebrafish | ACTIVE | |

```
$ openrc server show 4baf3781-bad8-4baf-86d5-3956f0cba88
$ openrc server show 4b7b729c-9de3-41b5-8691-d6ec3d5df74
```

| Field | Value |
|---|---|
| OS-EXT-DS:config | AUTO |
| OS-EXT-SVC:availability_zone | none |
| OS-EXT-SRV:power_state | 0 |
| OS-EXT-STS:task_state | None |
| OS-EXT-STS:vmm_power_state | None |
| OS-EXT-STS:vm_state | none |
| OS-SPF-WSG:terminated_at | None |
| accessIPv4 | None |
| accessIPv6 | None |
| config_drive | False |
| created | 2016-04-17T23:55:02 |
| flavor | [0 message: ' u no valid host was found. There are not enough hosts available.'; 0 code: 500; u created: u 2016-04-17T23:55:02 ] |
| hostId | 2b3a92e9f |
| id | 4baf3781-bad8-4baf-86d5-3956f0cba88 |
| image | [0 message: ' u no valid host was found. There are not enough hosts available.'; 0 code: 500; u created: u 2016-04-17T23:55:02 ] |
| key_name | None |
| OS-EXT-SRV-ATTR:host | None |
| OS-EXT-SRV-ATTR:hypervisor | 1 |
| OS-EXT-SRV-ATTR:raid | 1 |
| OS-EXT-SRV-ATTR:raid_id | 1 |
| project_id | 2b3a92e9d9f0bd94d102f88551b |
| properties | None |
| updated | 2016-04-17T23:55:02 |
| user_id | asd76b9b5754d04d3138424f615a |

### Debug Mode

In our deployment examples, we made a decision to turn debugging off. A change can be made in your `/etc/puppet/hiera/common.yaml` file in order to adjust debug level for each service and then you run the appropriate `puppet apply` command for that deployment scenario. Having debugging enabled is rarely the default because it produces a considerable number of logs that are unnecessary when a deployment is functioning normally. If you’re not using Puppet in your production deployment, you will want to refer to the documentation for each service to learn how to turn on debugging, but it will typically look something like this:

```
debug=True
```

As with any modification to a configuration file, we recommend that you make a backup of the configuration file you began with, even if you’re using a configuration management system. Having a starting point can help when you forget where you began or are seeking to pass off debugging to another engineer. You will then need to restart the respective service or services that are logging to that file for the debug change to take effect.

> **Tip**
> There are cases when debugging is left on for particular services for auditing or long-term debugging. Be aware of the problem spots in your infrastructure so you can make informed decisions about whether a service should run with debugging on long term or not.

### Understanding Log Messages

There are two main things you should keep in mind about OpenStack when reading log messages:

- It is written in Python, so you may encounter a lot of Python tracebacks, which provide stack trace information. As such, standard Python documentation on reading errors can be useful if the errors are not obvious to you.
- OpenStack is modular—it depends on various different components. When you see an error in one service, it may actually be due to a problem in another. We’ll dive into specifics of the likely candidates in the “Key Services” section of this chapter.

When debugging systems which are written in Python, a good general strategy is to first look at the last line in the traceback. This may give you a clear indicator of what went wrong. If the last line is not helpful, go to the top of the traceback and read through it for anything obvious.

If you don’t find anything in the traceback itself just yet, look at the lines in the log file above it. If you have debug enabled, you may need to sift through some lines to find actual errors. A command that a service depends on may be failing to complete successfully, you may have an authentication problem or perhaps there is an error about running out of resources, like memory. Once you find the error, having the debug lines
