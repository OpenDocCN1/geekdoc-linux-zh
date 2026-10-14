As your BitTorrent client is downloading parts of the file, other BitTorrent clients connect to your PC to download the parts that you’ve already retrieved. There’s no need to worry about that, though, because all of the interaction is happening within the confines of the BitTorrent client software. Your PC is protected from these remote connections doing any harm.

Once the BitTorrent software completely downloads the ISO image file, it continues to offer it for download to other clients. Proper BitTorrent etiquette dictates leaving your BitTorrent client running for a while so that you share your file parts with at least as many clients as you’ve used to retrieve them (called the *share ratio*).

# Verifying the File

After retrieving the entire LiveCD ISO image file, don’t celebrate just yet—there’s still one more step before you create your CD. With large file downloads, it’s quite possible that something somewhere along the way became corrupted. It’s a good idea to ensure that the file you’re about to use to install your operating system is valid.

Besides file corruption, there’s another thing you have to worry about. When you download an ISO image file from a server (especially a mirror server), you’re trusting that the people who created that file are trustworthy. Unfortunately, that’s not always the case. There are plenty of stories about attackers modifying ISO image files with malicious code and posting them on download servers.

The bottom line is that it’s a good idea to verify that the ISO image file you downloaded is the same as the original file posted by Ubuntu. Fortunately, there’s an easy way to do this.

# Using MD5 Sums

One way to verify the authenticity of a large file is with math. You can use a mathematical formula to evaluate the contents of the file before the download and compare those results with the results of the same formula after the download. If the results match, there’s a good chance that the file downloaded correctly and without modification.

The most common mathematical formulas used for this purpose are the *MD5* and *SHA1 hash algorithms*. Hash algorithms compute a unique, fixed-size result from any amount of data. If anything in the data changes, the hash algorithm result is different.

The MD5 algorithm generates a 128-bit value, usually represented as a 32-character hexadecimal value, often referred to as the *MD5 sum*. The SHA1 algorithm is more complex and generates a 160-bit value, represented as a 40-character hexadecimal value.

Ubuntu posts the MD5 sums for each of its download files in the general release page (http://releases.ubuntu.com/8.04) as the file MD5SUMS. These values are also kept on the web page https://help.ubuntu.com/community/UbuntuHashes. (Note that this is a secure https web site, and not a standard http site.)

The Ubuntu BitTorrent files each contain their own signed SHA1 sum. This file automatically downloads with the ISO image file from the BitTorrent site.

Once you’ve downloaded the hash files, you’ll want to perform the hash algorithm on your downloaded ISO image file and compare the values. The next section discusses just how to do this.