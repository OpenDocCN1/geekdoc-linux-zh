site. Snapshots are just points along the development branch; they undergo no special packaging or testing. Snapshots don’t receive the same attention to quality that releases do, but they’re intended as a good starting point for people interested on running -current or -stable. There’s only modest quality control, and many developers have no idea that a snapshot has come out until it appears on the FTP servers. You’ll find bugs. You’ll find errors. You’ll experience issues that will turn your mother’s hair white, assuming you haven’t done that to the poor woman already.

# # FreeBSD Support Model

With FreeBSD 11.0, the Project’s support model changed to more closely resemble that used by other commercial and noncommercial operating systems.

Each major release is supported with security and stability patches for five years after the first release. If FreeBSD 13 is released on January 1, 2021, support will end on January 1, 2026.

Each minor release is supported for three months after the release of the next minor release. Support for FreeBSD 12.3 will end three months after the release of FreeBSD 12.4. This gives you three months to schedule an upgrade.

A loss of official support doesn’t mean that you can’t continue to run unsupported versions. However, you’ll need to examine each security announcement, determine whether it affects your environment, and create your own patches. You’re better off running the upgrade.

The whole point of FreeBSD minor releases is that they’re minimally intrusive. Upgrading from FreeBSD 12.3 to 12.4 should have a similar impact to applying Windows updates or going from Centos 8.1 to 8.2. Applications should continue to run just fine.

The last FreeBSD minor release of a version gets supported and patched out to the five-year mark. If FreeBSD 12.5 is the last release of FreeBSD 12, it’ll get security patches out until five years after the release of FreeBSD 12.0.