# ## SELINUX

Traditional Linux security, called *Discretionary Access Control* (DAC), is based on users and groups. Because a process run by a user has access to anything the user has access to, fine-grained access control is difficult to achieve. Fine-grained access control is particularly important on servers, which often hold programs that require root privileges to run.

SELinux (Security Enhanced Linux), which was developed by the U.S. National Security Agency (NSA), implements *Mandatory Access Control* (MAC) in the Linux kernel. MAC enforces security policies that limit what a user or program can do. It defines a security policy that controls some or all objects, such as files, devices, sockets, and ports, and some or all subjects, such as processes. Using SELinux, you can grant a process only those permissions it needs to be functional, following the principle of least privilege (page 466). MAC is an important tool for limiting security threats that come from user errors, software flaws, and malicious users. The kernel checks MAC rules after it checks DAC rules.

SELinux can be in one of three states (modes):

+   * **Enforcing**—The default state, wherein SELinux security policy is enforced. No user or program will be able to do anything not permitted by the security policy.
+   * **Permissive**—The diagnostic state, wherein SELinux sends warning messages to a log but does not enforce the security policy. You can use the log to build a security policy that matches your requirements.
+   * **Disabled**—SELinux does not enforce a security policy because no policy is loaded.

Running SELinux in permissive or enforcing state degrades system performance somewhat. Although SELinux usually does not provide benefit on a single-user system, you may want to consider using SELinux on a server that connects to the Internet. If you are unsure whether to use SELinux, selecting permissive state allows you to easily change to disabled or enforcing state at a later date.

SELinux implements one of the following policies:

+   * **Targeted**—Applies SELinux MAC controls only to certain (targeted) processes (default).
+   * **MLS**—Multilevel Security protection.
+   * **Strict**—Applies SELinux MAC controls to all processes (*RHEL*).

This section discusses the targeted policy. With such a policy, daemons and system processes that do not have a specified policy are controlled by traditional Linux DACs. With the strict policy, all processes are controlled by SELinux (MACs). Setting up a system that runs under strict policy is beyond the scope of this book.