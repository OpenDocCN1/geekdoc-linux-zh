# Sample Scan

Earlier in this chapter, we performed a target discovery (during which we unearthed a network address); and now we have accumulated the right tools, so we're ready to perform a site scan. During this phase, we will scan only to discover active addresses and their open ports. Hackers would not spend a lot of time doing penetration scanning and vulnerability testing, as that could lead to their own detection.

A standard target site scan would begin with the assumption that the network is a full Class C (for a review of subnets, refer back to Chapter 1 and the appendixes in the back of this book). Thus, we'll set the scanner for an address range of 206.0.126.1 through 206.0.126.254, and 24 bits in the mask, or 255.255.255.0, to accommodate our earlier DNS discovery findings:

www www.xyzinc.com 206.0.126.10

mail mail.xyzinc.com 206.0.126.11

ftp ftp.xyzinc.com 206.0.126.12

For the first pass, and for maximum scanning speed, we'll scan ports 1 to 1000 (most of the well-known ports):

+   206.0.126.1  206.0.126.55  206.0.126.96

+   206.0.126.8  206.0.126.56  206.0.126.97

+   206.0.126.10:80  206.0.126.61  206.0.126.110

+   206.0.126.11  206.0.126.62  206.0.126.111

+   206.0.126.22  206.0.126.63  206.0.126.112

+   206.0.126.23  206.0.126.64  206.0.126.113

+   206.0.126.25  206.0.126.65  206.0.126.114

+   206.0.126.27  206.0.126.66  206.0.126.115

+   206.0.126.28  206.0.126.67  206.0.126.116

+   206.0.126.29  206.0.126.69  206.0.126.117

+   206.0.126.30  206.0.126.70  206.0.126.118

+   206.0.126.33  206.0.126.86  206.0.126.119

+   206.0.126.35  206.0.126.87  206.0.126.120

+   206.0.126.39  206.0.126.89  206.0.126.121

+   206.0.126.44  206.0.126.92  206.0.126.122

+   206.0.126.49  206.0.126.93  206.0.126.123

+   206.0.126.53  206.0.126.94  206.0.126.124

+   206.0.126.54  206.0.126.95  206.0.126.125

+   206.0.126.126  206.0.126.158  206.0.126.223

+   206.0.126.127  206.0.126.159  206.0.126.224

+   206.0.126.128  206.0.126.168  206.0.126.225

+   206.0.126.129  206.0.126.172  206.0.126.231

+   206.0.126.130  206.0.126.173  206.0.126.236

+   206.0.126.131  206.0.126.175  206.0.126.237

+   206.0.126.133  206.0.126.177  206.0.126.238

+   206.0.126.136  206.0.126.179  206.0.126.239

+   206.0.126.137  206.0.126.183  206.0.126.240