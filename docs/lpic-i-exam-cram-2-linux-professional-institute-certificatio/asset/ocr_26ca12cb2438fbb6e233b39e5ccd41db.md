the service under inetd or xinetd control. Anytime you put services behind inetd or xinetd, they must be started to function, and that means a small though noticeable delay—often enough that a client request times out.

# The hosts.allow and hosts.deny Files

The two tables that affect which clients can connect to which services (provided the service uses libwrap.a or is controlled by inetd/xinetd) are /etc/hosts.allow and /etc/hosts.deny.

The format of a typical hosts.allow or hosts.deny file is as follows:

*daemons : hosts : option : option*

Daemons or services can be specified several ways, including

+   - ALL—This means just that, all services.

+   - *service*—A single service name affects only that service.

+   - *daemon, daemon*—Multiple daemons affected by an entry should be separated by spaces or commas.

Hosts can be specified by many methods, including

+   - *hostname*—This affects a single unqualified hostname, typically from the local domain.

+   - *hostname.example.com*—This affects a resolvable, fully qualified hostname, typically from a remote domain.

+   - *@group*—This is used by NIS to denote a Net group and is unlikely to appear on the exam.

+   - 10.1.1.0/255.255.255.0—This notation affects the hosts 10.1.1.1–10.1.1.255. The /XX notation for bits can be used, too, such as /24 to denote a default Class C subnet mask.

+   - */path/filename*—This causes the listed file (full path and filename) to be referred to as the list of hosts that will be affected.

# Wrapper Read Order

The following rules are important to understand when using TCP wrappers to protect services:

+   - **The /etc/hosts.allow file is read and parsed first**—Any matches in it cause access to be allowed, skipping the /etc/hosts.deny file entirely.