
<= end of example page =>

This site contains lots of things to download but currently we are only interested in the kernel. Point your browser at the kernel directory.
Something like this should show:

<= start of example page =>

Index of /pub/linux/kernel
| Name | Last modified | Size | Description |
| :--- | :--- | :--- | :--- |
| [DIR] Parent Directory | 31-Dec-98 | 09:05:57 | - |
| [ ] COPYING | 16-Sep-99 | 00:00 | 18k | - |
| [ ] CHECKS | 18-Dec-98 | 20:55:55 | - |
| [DIR] History/ | 18-Dec-98 | 09:45:04 | - |
| [DIR] alsa/ | 18-May-99 | 10:55:15 | - |
| [DIR] drivers/ | 27-Jan-99 | 00:55 | - |
| [DIR] hpa/ | 19-Dec-98 | 02:16 | - |
| [DIR] peci2/ | 18-May-99 | 21:55:55 | - |
| [DIR] testing/ | 27-May-99 | 08:55:55 | - |
| [DIR] v1.0/ | 19-Dec-98 | 02:19 | - |
| [DIR] v1.1/ | 19-Dec-98 | 08:51:55 | - |
| [DIR] v1.2/ | 18-Dec-98 | 08:36:33 | - |
| [DIR] v1.3/ | 19-Dec-98 | 13:21 | - |
| [DIR] v2.0/ | 11-Feb-99 | 16:48 | - |
| [DIR] v2.1/ | 11-Feb-99 | 19:45:55 | - |
| [DIR] v2.2/ | 24-Mar-99 | 00:27 | - |
| [DIR] whaves/ | 18-Dec-98 | 19:34 | - |

Linux kernel release 2.0.0

These are the release notes for linux version 2.0. Read them carefully, as they tell what this is all, explain how to install the kernel, and what to do if something goes wrong.

...

<= end of example page =>

For our example we will take in consideration while writing this kernel version 2.2.x series is the stable version. That's why we choose the v2.2/ directory on the server.
How do you know which is the latest version? At the bottom of the http://www.kernel.org/ page you have a text like this:

<= start of example page =>

# The latest stable version of the Linux kernel is:

2.2.12

The latest beta version of the Linux kernel is:

2.3.20

The latest prepatch (alpha) version appears to

none

<= end of example page =>

That is your information to find which is the latest stable kernel and which one is recommended to use. Also as you will see you usually see a file with the name LATEST-IS-2.2.12 at the top of the directory list which tells you the latest version.

Once that we are in the v2.2/ directory on our server we will see something like this:

Index of /pub/kernel/v2/

| Name | Modified | Size | Description |
| :--- | :--- | :--- | :--- |
| [DIR] Parent Directory | 16-Aug-99 | 09:13 | - |
| [ LATEST-IS-2.2.12 | 26-Jun-99 | 02:45 | 04k |
| [ linux-2.2.0.tar.bz2 | 26-Jun-99 | 02:41 | 10.1M |
| [ linux-2.2.0.tar.gz | 26-Jun-99 | 02:41 | 125k |
| [CMP] linux-2.2.0.tar.gz | 26-Jun-99 | 02:41 | 12.5M |
| [ linux-2.2.1.tar.bz2 | 28-Jan-99 | 21:56 | 10.1M |
| [ linux-2.2.1.tar.gz | 28-Jan-99 | 21:56 | 125k |
| [CMP] linux-2.2.1.tar.gz | 28-Jan-99 | 21:56 | 12.5M |
| [ linux-2.2.10.tar.bz2 | 14-Jul-99 | 07:33 | 13.3M |
| [ linux-2.2.10.tar.gz | 14-Jul-99 | 07:33 | 138k |
| [CMP] linux-2.2.10.tar.gz | 14-Jul-99 | 07:33 | 13.3M |
| [ linux-2.2.11.tar.bz2 | 03-Aug-99 | 01:03 | 11.2M |
| [ linux-2.2.11.tar.gz | 03-Aug-99 | 01:03 | 138k |
| [CMP] linux-2.2.11.tar.gz | 03-Aug-99 | 01:03 | 13.8M |
| [ linux-2.2.12.tar.bz2 | 26-Aug-99 | 02:46 | 9.5M |
| [ linux-2.2.12.tar.gz | 26-Aug-99 | 02:46 | 104k |
| [CMP] linux-2.2.12.tar.gz | 26-Aug-99 | 02:46 | 9.5M |
| [ linux-2.2.23.tar.bz2 | 23-Feb-99 | 03:58 | 10.1M |
| [ linux-2.2.23.tar.gz | 23-Feb-99 | 03:58 | 125k |
| [CMP] linux-2.2.23.tar.gz | 23-Feb-99 | 03:58 | 10.1M |
| [ linux-2.2.24.tar.bz2 | 23-Mar-99 | 23:33 | 10.4M |
| [ linux-2.2.24.tar.gz | 23-Mar-99 | 23:33 | 131k |
| [CMP] linux-2.2.24.tar.gz | 23-Mar-99 | 23:33 | 10.4M |
| [ linux-2.2.25.tar.bz2 | 29-Mar-99 | 08:54 | 10.4M |
| [ linux-2.2.25.tar.gz | 29-Mar-99 | 08:54 | 125k |
| [CMP] linux-2.2.25.tar.gz | 29-Mar-99 | 08:54 | 12.5M |
| [ linux-2.2.26.tar.bz2 | 16-Apr-99 | 23:46 | 10.5M |
| [ linux-2.2.26.tar.bz2_s | 16-Apr-99 | 23:46 | 16k |
| [CMP] linux-2.2.26.tar.gz.sign | 16-Apr-99 | 23:46 | 13.0M |
| [ linux-2.2.26.tar.gz.sign | 16-Apr-99 | 23:46 | 1k |
| [ linux-2.2.27.tar.bz2_s | 28-Apr-99 | 20:42 | 10.6M |
| [ linux-2.2.27.tar.bz2_s | 28-Apr-99 | 20:42 | 1M |
| [CMP] linux-2.2.27.tar.gz.sign | 28-Apr-99 | 20:42 | 13.0M |
| [ linux-2.2.27.tar.gz.sign | 28-Apr-99 | 20:42 | 10.6M |
| [ linux-2.2.28.tar.bz2_s | 11-May-99 | 21:59 | 10.7M |
| [ linux-2.2.28.tar.bz2_s | 11-May-99 | 21:59 | 1M |
| [CMP] linux-2.2.28.tar.gz.sign | 11-May-99 | 21:59 | 13.2M |
| [ linux-2.2.28.tar.gz.sign | 11-May-99 | 21:59 | 19.1M |
| [ linux-2.2.29.tar.bz2_s | 14-May-99 | 01:54 | 10.7M |
| [ linux-2.2.29.tar.bz2_s | 14-May-99 | 01:54 | 1M |
| [DIR] Parent Directory | 16-Aug-99 | 09:13 | - |
| [ 2.2.0.tar.bz2_s | 26-Aug-99 | 02:42 | 10.1M |
| [ 2.2.0.tar.bz2_s | 26-Aug-99 | 02:42 | 1M |
| [CMP] 2.2.0.tar.gz.sign | 26-Aug-99 | 02:42 | 13.5M |
| [ 2.2.0.tar.gz.sign | 26-Aug-99 | 02:42 | 10.1M |
| [ 2.2.1.tar.bz2_s | 28-Jun-99 | 21:56 | 10.1M |
| [ 2.2.1.tar.bz2_s | 28-Jun-99 | 21:56 | 1M |
| [CMP] 2.2.1.tar.gz.sign | 28-Jun-99 | 21:56 | 12.5M |
| [ 2.2.1.tar.gz.sign | 28-Jun-99 | 21:56 | 10.1M |
| [ 2.2.10.tar.bz2_s | 14-Jul-99 | 07:33 | 10.8M |
| [ 2.2.10.tar.bz2_s | 14-Jul-99 | 07:33 | 1M |
| [CMP] 2.2.10.tar.gz.sign | 14-Jul-99 | 07:33 | 13.3M |
| [ 2.2.10.tar.gz.sign | 14-Jul-99 | 07:33 | 10.8M |
| [ 2.2.11.tar.bz2_s | 03-Aug-99 | 01:03 | 11.2M |
| [ 2.2.11.tar.bz2_s | 03-Aug-99 | 01:03 | 1M |
| [CMP] 2.2.11.tar.gz.sign | 03-Aug-99 | 01:03 | 13.8M |
| [ 2.2.11.tar.gz.sign | 03-Aug-99 | 01:03 | 11.2M |
| [ 2.2.12.tar.bz2_s | 26-Aug-99 | 02:45 | 10.6M |
| [ 2.2.12.tar.bz2_s | 26-Aug-99 | 02:45 | 1M |
| [CMP] 2.2.12.tar.gz.sign | 26-Aug-99 | 02:45 | 13.0M |
| [ 2.2.12.tar.gz.sign | 26-Aug-99 | 02:45 | 10.6M |
| [ 2.2.22.tar.bz2_s | 23-Sep-99 | 05:58 | 10.1M |
| [ 2.2.22.tar.bz2_s | 23-Sep-99 | 05:58 | 1M |
| [CMP] 2.2.22.tar.gz.sign | 23-Sep-99 | 05:58 | 13.2M |
| [ 2.2.22.tar.gz.sign | 23-Sep-99 | 05:58 | 10.1M |
| [ 2.2.23.tar.bz2_s | 09-Mar-99 | 09:42 | 10.2M |
| [ 2.2.23.tar.bz2_s | 09-Mar-99 | 09:42 | 1M |
| [CMP] 2.2.23.tar.gz.sign | 09-Mar-99 | 09:42 | 13.1M |
| [ 2.2.23.tar.gz.sign | 09-Mar-99 | 09:42 | 10.2M |
| [ 2.2.24.tar.bz2_s | 23-Jan-99 | 23:33 | 10.6M |
| [ 2.2.24.tar.bz2_s | 23-Jan-99 | 23:33 | 1M |
| [CMP] 2.2.24.tar.gz.sign | 23-Jan-99 | 23:33 | 13.2M |
| [ 2.2.24.tar.gz.sign | 23-Jan-99 | 23:33 | 10.6M |
| [ 2.2.25.tar.bz2_s | 29-Mar-99 | 08:54 | 10.4M |
| [ 2.2.25.tar.bz2_s | 29-Mar-99 | 08:54 | 1M |
| [CMP] 2.2.25.tar.gz.sign | 29-Mar-99 | 08:54 | 13.0M |
| [ 2.2.25.tar.gz.sign | 29-Mar-99 | 08:54 | 10.4M |
| [ 2.2.55.tar.bz2_s | 20-Aug-99 | 08:54 | 10.4M |
| [ 2.2.55.tar.bz2_s | 20-Aug-99 | 08:54 | 1M |
| [CMP] 2.2.55.tar.gz.sign | 20-Aug-99 | 08:54 | 13.0M |
| [ 2.2.55.tar.gz.sign | 20-Aug-99 | 08:54 | 10.4M |
