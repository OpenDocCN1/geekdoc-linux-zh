
## ACL OPTIONS

ACL Options provide some additional features that can be used when the Access Control List system is enabled through Grsec. Some options are set based on your policy, such as password lockout for the ACL system.

**Recommendation:**

If you're going to be using the Grsec ACL system, set these options as appropriate for your environment.

## FILESYSTEM PROTECTIONS

The Filesystem Protections provided by Grsec enable the additional **chroot** restrictions that should be used if you're running applications in a **chroot**. Other protections are also provided within this option area, including restrictions on symlinks, the proc filesystem, and FIFO restrictions.

**Recommendation:**

You can greatly enhance security by enabling these options, especially including the **chroot** options if you're using **chrooted** applications.

## KERNEL AUDITING

A group of options that provides useful logging and tracking options can be found within the Kernel Auditing area. Included within this area are such things as logging for time changes, filesystem mounting and unmounting, and even logging every call to the **execve()** system. Some of these options can create huge log files but are invaluable when performing forensics on a successful attack.

**Recommendation:**

Enable as many of these options as possible. However, be careful not to fill up your log directory filesystems because of the number of entries created with things like **Exec Logging**.

## EXECUTABLE PROTECTIONS

Four important options appear within Executable Protections. These include options to prevent local users from possibly gaining extra privilege or gathering information about the system. Even if you aren't intending to allow 'shell' (think: command-line) access to users on the system, an attacker's goal in life is to gain that shell access. These options can help prevent the attacker from gaining additional privileges if the attacker happens to gain shell access.

**Recommendation:**

Enable these options if possible in your environment.

## NETWORK PROTECTIONS

Providing a broad range of helpful additional security are the Network Protections within Grsec. Randomization is a key component of these protections and can make it more difficult for an automated scan or probe to identify your operating system.

**Recommendation:**

Enable as many of these options as possible in your environment.

## SYSECTL SUPPORT

Using Sysectl, you can enable many of the features of Grsec individually to help in troubleshooting. This is particularly helpful when you're first using Grsec in case an application won't start and you believe it to be because of a Grsec option. Using Sysectl, you issue an **echo** command to enable some of the various features that were compiled into the Grsec kernel. When you have a stable system, you then issue another **echo** command to effectively “lock” the environment, preventing the Grsec features from being disabled without a reboot. If you fail to lock the environment and you don't recompile to disable Sysectl support, an attacker can remove the Grsec protections, thus making them useless!

**Recommendation:**

Enable Sysectl support when first getting acquainted with Grsec. When you have a system that is stable with the various Grsec options that you've chosen, recompile the kernel to remove Sysectl support. Failure to do so can completely negate any Grsec enhancements.

## LOGGING OPTIONS

The Logging Options area controls the performance of Grsec logging. Within this area you'll find options to configure the number of messages that can be sent within a certain (configurable) time period. This can help prevent possible denial-of-service attacks resulting from an attacker causing log file filesystems to fill up or creating noisy logs.

**Recommendation:**

Set these options as appropriate for your environment.

## Building the Grsec Kernel

Building the kernel with Grsec is, in effect, no different from building another kernel. You've already applied the patch and, hopefully, chosen the options you would like to try. From here, back up to earlier in the chapter and follow the instructions for compiling the kernel from source.

# CHAPTER 13: Kernel Enhancements

After you've compiled the kernel and restarted, you can begin testing the new environment. The first thing to do is to make sure that the Grsec kernel is actually running. This task is accomplished by typing this:

```
uname -a
```

You should see output containing a portion similar to the following:

```
2.4.25-grsec
```

Obviously, the kernel revision number will probably be different, but the key is to ensure that grsec appears in that name. If it does, you're running with a Grsec kernel. If it doesn't, you should examine why the kernel booted to a different version other than the one you compiled. This could be because you forgot to run Lilo or forgot to install the kernel as the final step of the compile. Refer to the section “Compiling Your First Kernel” for possible causes.

If you've chosen to enable Syctl support so that you can enable and disable certain Grsec features on the fly, you'll find a number of files located in the /proc/sys/kernel/grsecurity directory. You can enable these options within Grsec by typing this:

```
echo 1 > /proc/sys/kernel/grsecurity/<filename>
```

Here, <filename> is the name of the option as found by doing a ls within /proc/sys/kernel/grsecurity. For example, if you want to enable the randomized process IDs (PIDs), the file is called *rand_pids*. You'd enable it with this line:

```
echo 1 > /proc/sys/kernel/grsecurity/rand_pids
```

After this particular option is enabled, you can run the *ps* command and watch new processes as they are created. They will have pseudo-random ID numbers rather than the traditional incrementing PIDs. I'd probably use the command *ps aux* as root to see all the processes.

To disable a Grsec feature, simply *echo 0* to the file. For example, to disable the PID randomization that you just enabled, run the following command:

```
echo 0 > /proc/sys/kernel/grsecurity/rand_pids
```

It's important to remember that until you “lock” the Grsec features, an attacker can undo those features. The drawback is that after you lock the features, you can't undo them yourself without rebooting the computer. By locking, you prevent other features from being enabled or disabled until the server is rebooted, and this applies only if you're using the Syctl option within Grsec. Lock the features with this command:

```
echo 1 > /proc/sys/kernel/grsecurity/grsec_lock
```

## Beyond the Basics with GrSecurity

I’ve only scratched the surface of the benefits of GrSecurity. One of the greatest benefits of Grsec is its capability to enhance the available permissions on a file, known as Role Based Access Control (RBAC). Windows administrators who are familiar with and use the Advanced permissions that can be given to a file in Windows will want to explore these features in Grsec as well. This chapter has examined only the kernel patch portion of Grsec. There is also administration software for RBAC called gradm that enables a large set of specialized file and object permissions.

More information on the GrSecurity ACL system can be found on the GrSecurity website at http://www.grsecurity.net/gracledoc.htm.

## Conclusion: Custom Kernels

This chapter covered an important topic and one that is vital for a good Linux administrator to know, namely, compiling a custom kernel. Custom kernels enhance security by enabling the administrator to choose only those options necessary for the specific computer on which the kernel will reside. By disabling unnecessary drivers and module support, you can reduce the number of attack paths available for an exploit.

Using a security-enhanced kernel such as a kernel with SELinux or a GrSecurity kernel significantly decreases the risk posed by some of the more advanced exploit techniques available. As with other security options, GrSecurity provides only one facet of a host’s security. Without things like *chroot*, and even simply keeping the server patched, Grsec won’t be as helpful. However, for all the benefits that Grsec can provide, it should be used whenever possible. It’s worth the time and effort and is certainly a much better option than cleaning up after an attack that could’ve been prevented.
