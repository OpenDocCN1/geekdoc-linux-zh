# # INTRODUCTION

This is the Linux IPChains-HOWTO. You should also read the Linux NET-3-HOWTO (see Chapter 8), the IP Masquerading HOWTO (see Chapter 12), the PPP HOWTO (see Chapter 9), the Ethernet HOWTO (see http://metalab.unc.edu/LDP/), and the Firewall HOWTO (http://metalab.unc.edu/LDP/). (Then again, so might the alt.fan.bigFoot FAQ.)

If packet filtering is passe to you, read the “Why?” and “How?” sections later in this chapter and scan through the titles in the “IP Fire-walling Chains” also later in this chapter.

If you are converting from ipfwadm, read the “What,” “How” “Differ-ences between ipchains and ipfwadm,” and “Using the ipfwadm-wrapper Script” sections later in this chapter.

# ## What?

Linux ipchains is a rewrite of the Linux IPv4 firewalling code (which was mainly stolen from BSD) and a rewrite of ipfwadm, which was a rewrite of BSD’s ipfw, I believe. It is required to administer the IP packet filters in Linux kernel versions 2.1.102 and above.

# ## Why?

The older Linux firewalling code doesn’t deal with fragments; has 32-bit counters (on Intel at least); doesn’t allow specification of protocols other than TCP, UDP or ICMP; can’t make large changes atomically; can’t spec-ify inverse rules; has some quirks; and can be tough to manage (making it prone to user error).

# ## How?

Currently the code is in the mainstream kernel from 2.1.102. For the 2.0 ker-nel series, you will need to download a kernel patch from the Web page. If your 2.0 kernel is more recent than the supplied patch, the older patch should be OK; this part of the 2.0 kernels is fairly stable (that is, the 2.0.34 kernel patch works just fine on the 2.0.35 kernel). Since the 2.0 patch is incompatible with the ipportfw and ipautosfw patches, I don’t recom-mend applying it unless you really need the functionality that ipchains offer.