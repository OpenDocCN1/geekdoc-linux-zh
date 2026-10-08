# Red Hat Alerts

Red Hat is more than just Red Hat Enterprise Linux (RHEL). While RHEL is the flagship Red Hat distribution, it's not the only option associated with Red Hat software. This book lists two major alternatives to RHEL: Fedora and CentOS Linux. Unfortunately, it is patently unfair to many other distributions that use Red Hat software and Red Hat–style packages.

Red Hat Enterprise Linux

For RHEL, two methods are available for monitoring security advisories. The public Red Hat security advisories (RHSAs) mailing list, and the list of errata on the Red Hat Network (RHN). Anyone with an e-mail address can sign up for the RHSA mailing list at https://www.redhat.com/mailman/listinfo/rhsa-announce!. An equivalent Simple Syndication (RSS) feed is also available. Anyone with a subscription to the RHN can access the errata, with associated security advisories. The information on both lists is essentially the same.

However, anyone with a paid subscription can download the binary packages from the RHN that can automatically download and install such updates. Any system that connects to the RHN can be configured to do this updates. More options for pulling and pushing such updates are described later in this chapter.

If you find a security issue with an RHEL system, Red Hat encourages you to contact its Security Response Team at alert@redhat.com. For https://www.redhat.com/security/team/, e-mails sent to are kept confidential if you desire.

In their efforts to provide enterprise-level support, Red Hat provides security updates for its RHEL releases for at least seven years.

# CentOS Linux

The developers of CentOS use the RHEL source code released by Red Hat under open source licenses. As such, the CentOS distribution is known as a rebuild of RHEL. Most security issues with CentOS software also apply to Red Hat software. But there are differences. To avoid trademark issues, CentOS modifies some RHEL source code to omit RHEL trademarks.

Many Linux use CentOS, as there is no charge for access to that distribution in its binary format. Of course, CentOS cannot offer Red Hat support for its distribution. And there's commonly a time lag between the release of a Red Hat security update and a CentOS security update.

CentOS updates its distribution a little while when updated RHEL source code is publicly released. It takes a little while for the volunteers behind CentOS to compile the source code and test it on the CentOS rebuild distribution.

CentOS also has a mailing list for security advisories at http://lists.centos.org/mailman/listinfo/centos-announce/. Equivalent information is also made on CentOS message boards. CentOS advisories and updated packages typically lag behind those associated with Red Hat by a few days. But of course, CentOS is more freely available than Red Hat.