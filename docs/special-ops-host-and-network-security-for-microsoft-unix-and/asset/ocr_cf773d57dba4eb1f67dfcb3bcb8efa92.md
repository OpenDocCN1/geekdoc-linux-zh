# Assessing Internal Network Security · Chapter 1

Keep in mind the following points after installing a golden build operating system:

+   * Remove default services that are not required.
* Set file and directory permissions (especially on multi-user systems).
* Install third-party applications and specify them by version and required patches.
* Use host-level access control mechanisms such as ipchains, Windows XP’s Internet Connection Firewall (ICF), or IPSec as another layer of defense should network level access control lists (ACLs) fail.

**Audit your work.** The auditor in forces me to recommend that you create an audit trail during and after the system creation. A simple checklist and sign-off should do the trick for smaller environments, but in larger environments, a full lifecycle may be required. This is just like a software development lifecycle (SDLC) and will likely require multiple groups to get the server rolled out.

+   * **Ensure integrity.** Although this may seem obvious, be sure to keep all media used for installations in a secure location. If a disgruntled employee was able to modify your gold build with a Trojan, you would have a serious problem on your hands. MD5 checksums and signed encryption techniques can be used to ensure integrity. Products such as those offered by TripWire can be used to verify the file integrity of systems and build builds, or the integrity of routers and switches.

+   **Know when to rebuild.** Finally, be sure to clearly define what circumstances require a system rebuild.Rebuilding a box due to a false alarm can be just as costly as *not* rebuilding one that has been compromised.

# Security Checklist

+   * If necessary, build security awareness of executives to get buy-in.
* If necessary, learn your organization. This is paramount.
* Build a project team involving each part of your organization.
* Enumerate each business operation and its resources.