310

# Mirroring

Mirroring is used for creating a "carbon copy" of a live directory structure on another live system. This is normally a means of providing an alternate computer with the same information in case the computer you're using becomes unavailable (whether "it went down" from too heavy a CPU load or other miscellaneous reasons). For example, many Web sites are mirrored; if one of them gets too busy, the traffic can go in another direction with minimal interruption. These mirrors are updated anywhere from weekly, daily, or hourly intervals.

You can find the mirroring tool Mirrorird and FTP Backup Utility on the Web at http://sunsite.unc.edu/pub/linux/system/backup. Mirroird mirrors links, devices, permissions, ownerships, access times, and any other aspect of the mirror site's files via FTP. It also provides revision control, and works well with timed backups.

![](bbox=[0.16, 0.41, 0.24, 0.48])

You may want to consider the use of mirroring as a backup utility in its own right, especially if you use Mirroird to create an emergency site.

# Emergency Live Backup Site

If you are running Linux as a personal computer at home, you probably don't need to worry about having a live backup site. However, for a business, an emergency site enables you to continue computing activity once the original site goes down. For example, California is known to have frequent earthquakes. You may want to have a live backup site in Indiana where earthquakes or other natural disasters are less likely to strike.

Though business at the California site will come to a standstill in the event of a serious earthquake, you can still continue conducting business through the Indiana live site.

Depending on the type of business you are doing, you may need to keep a live site to keep like accounting and payroll systems active and make sure those affected by the disaster can keep functioning.

# Off-Site Storage of Critical Files

For most administrators, whether business and personal Linux users, off-site storage of critical files such as log archives and backups is ideal. If someone breaks into your house and steals your computer, have a way to get access back to your files. If your hard drive at work crashes, and you can't get access to those backed-up alpha releases, and the local backups are corrupt, you may want to store the files at an off-site facility.