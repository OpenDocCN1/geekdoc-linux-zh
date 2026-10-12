![](bbox=[0.18, 0.07, 0.76, 0.23])

# Figure 4.3 Network layout

a class B to an organization that is large but doesn’t need the 65,536 IP addresses that a full class B offers. This is called Classless Inter-Domain Routing (CIDR). It’s almost universal now – it’s used on the Internet backbone, and on all Windows and Linux systems. The old class-based system continues only in some historical protocols and throughout this book we deal exclusively with CIDR.

Conveniently (and it’s not a coincidence – this compatibility was designed into the system) you can exactly duplicate the old class A, B, C behavior by considering each class as specifying a default netmask:

| Class | Default netmask |
| :--- | :---: |
| A | 255.0.0.0 |
| B | 255.255.0.0 |
| C | 255.255.255.0 |

In many contexts both Windows-NT and Linux will assume these default netmasks when you enter an address and don’t specify an explicit netmask. Just think of classes as a convenient notation and nothing more.