Notice also in that last argument that there is a needed colon (`:`) between the IPv4 address and the directory symbol. If you do not include this colon, you will copy the files to a new file named `user1@192.168.0.104~` in the local directory.

![](bbox=[0.14, 0.18, 0.22, 0.25])

> The `rsync` utility uses OpenSSH by default. However, it's good practice to use the `-e` option. This is especially true if you are using any `ssh` command options, such as designating an OpenSSH key to employ or using a different port than the default port of 22. OpenSSH is covered in more detail in Chapter 16, “Looking at Access and Authentication Methods.”

The `rsync` utility can be handy for copying large files to remote media. If you have a fast CPU but a slow network connection, you can speed things up even more by employing the `rsync -z` option to compress the data for transfer. This is not using `gzip` compression but instead applying compression via the `zlib` compression library. You can find more out about `zlib` at `https://zlib.net`.

# ## Securing Offsite/Off-System Backups

In business, data is money. Thus it is critical not only to create data archives but also to protect them. There are a few additional ways to secure your backups when they are being transferred to remote locations.

Besides `rsync`, you can use the `scp` utility, which is based on the Secure Copy Protocol (SCP). Also, the `sftp` program, which is based on the SSH File Transfer Protocol (SFTP), is a means for securely transferring archives. We’ll cover both utilities in the following sections.

# ### Copying Securely via `scp`

The `scp` utility is geared for quickly transferring files in a noninteractive manner between two systems on a network. This program employs OpenSSH.

It is best used for small files that you need to securely copy on the fly, because if it gets interrupted during its operation, it cannot pick back up where it left off. For larger files or more extensive numbers of files, it is better to employ either the `rsync` or the `sftp` utility.

There are some rather useful `scp` options. A few commonly used switches are listed in Table 12.6.