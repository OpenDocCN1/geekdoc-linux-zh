# ETHEREAL HOME PAGE

Your SLES installation comes with a version of Ethereal. Information on how to run it can be found in the local man pages.

You will probably want to visit the Ethereal home page to get an up-to-date version of the product. As new versions are introduced, it will be important to keep up the documentation supplied. You can find the Ethereal home page at http://www.ethereal.com.

Keep in mind that written authorization by an individual who is allowed to give such permission should be obtained before this tool is used on any network.

Ethereal can be quite intrusive in terms of data privacy. Packets containing cleartext data can easily be reconstructed and sensitive information divulged. This is why most corporate IT security policies emphatically state that such applications are forbidden. In the proper hands and in the right circumstances, Ethereal can allow you to solve a myriad of network issues.

# Summary

After reading this chapter, you should have a good comfort level with the concept of both host- and network-based intrusion detection systems. The tools presented here are all part of the SLES environment. Deploying these solutions can vastly improve your chances of detecting unwelcome visitors.

The tools presented here are an essential part of a proper HIDS and NIDS environment. On the host intrusion side, you saw tools that are capable of determining whether changes have been made to the content of the filesystem. You also saw other tools that can be used to monitor port scans of your systems.

On the network side, you looked at tools such as Snort and ACID and how you can use them to raise alerts when suspicious traffic is detected. You can watch for abnormal network loads using tools such as MRTG and Cacti. Such traffic can alert you to network threats that might be compromised or at the very least are behaving in an unexpected fashion.

All these tools participate together in protecting your environment and contribute to a robust, layered defense against attacks.

The most difficult portion of intrusion detection is fine-tuning the various solutions. Improperly tuned environments generate a large number of false-positive results. This can lead to situations in which valid results are missed. Alternately, solutions that have been overtuned may become blind to a whole family of attack mechanisms.