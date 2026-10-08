# Chapter 28: Backing Up and Restoring Files

If you selected the Zip or Tar archive options, the BackupPC application displays your Web browser's standard file download dialog after the archive file has been created.

As you can see from this section (and the preceding sections), BackupPC provides a powerful, flexible interface for backing up and restoring files on many different systems to a single backuppc. All you need is a few configuration files and sufficient disk space, and lost files (the lost that is usually associated with them) can be a thing of the past.

# Backing Up and Mirroring to the Cloud with Ubuntu One

One of today's hottest buzzrases is "cloud computing," which is the common name for a variety of ways of delivering hosted services that depend on the Internet (the "cloud”). Cloud computing encompasses a number of different hosted service models, including:

+   - Infrastructure-as-a-Service (IaaS), where you use, configure, and access virtual computer systems over the Internet
- Storage-as-a-Service (SaaS), where you store file and folder on remote storage over the Internet. The best known platform-independent examples of these are Amazon's Simple Store (S3, http://www.amazon.com/s3), Dropbox (https://www.dropbox.com), and Canonical's Ubuntu One (https://one.ubuntu.com).
- Software-as-a-Service (the most common name of SaaS), where you access software over the Internet rather than installing it on your local computer system. The best known example of this type of software at the enterprise level is Salesforce.com. The best free example of this at the personal (and business) levels is Google Apps (www.google.com/apps).

There are plenty of other cloud business models, but these are the basics. Frankly, I find the idea of storing my critical data on someone else's machine somewhere on the Internet and accessing that data via remote applications to be completely scary. Believe it or not, I occasionally work on documents, spreadsheets, presentations, listen to music, and watch videos in locations where I have no access to the Internet. I'm not sure that "my network connection was down" is going to fly as an excuse for missed homework assignments more than "my dog ate my homework" when I was a kid. Similarly, storing personal data on remote systems may introduce privacy issues, meaning that government or specific three-letter-acronym agencies may have the right to examine your data if they decide to investigate the case that is hosting your cloud data should always read the fine print regarding personal data protection before hosting data on someone else's system!

Regardless of how you feel about cloud computing (whether you care at all), Storage-as-a-Service is inherently useful as a way of accessing your files from multiple computer systems without transferring them back and forth between each system on which you want to use them. Even