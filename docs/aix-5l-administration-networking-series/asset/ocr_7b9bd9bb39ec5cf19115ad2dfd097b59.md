Since you are reading this book, you are without a doubt going to manage AIX systems. The most important chapter in this book is this chapter. A thorough understanding of the storage hardware and the Logical Volume Manager (LVM) and its components is vital to effective AIX system management. I want to start this chapter with the hardware components and then move into the components of the Logical Volume Manager (LVM) and the terminology that we use.

# # DISK EVOLUTION

Are your filesystems half full, or are they half empty? It doesn't matter how much disk space you throw into a system. They are always half full and growing fast! A typical AIX 5L installation with DocSearch installed is about 2.75 gigabytes (GB) for a base installation. A more valid size for all of the extra toys is on the order of 4GB of unmirrored space. (Always mirror the *root volume group*) If you have been around computer systems for a long time like I have, you may remember when 10MB hard drives on an IBM PC/XT seemed like more storage than you could ever use. Today the IBM pSeries machines ship with 32GB and 72GB hard drives, and 128GB and 256GB drives are coming fast.

# # DISKS ARE DOUBLING EVERY SIX MONTHS

As I stated in the previous section, the IBM pSeries machines are shipping with 32GB and 72GB drives. The transition to twice the disk space occurred in only six months! Of course this disk technology has been in the works for years. The evolution is possible because of two main factors: The disk drive head is getting much smaller, and the platter technology keeps getting better. The disk drive heads are getting as small as the surface mount electronic components that you see on circuit boards.

A drive head in the 1980s was the size of your fingernail, but the disk drive could only hold about 10MB of data. The smaller and smaller heads allow for finer granularity of the disk platter. The disk platter technology is moving to better platter material, and many companies are doing research and development on plastic disk drives. The plastic platter is coated with a magnetic substrate to give the plastic magnetic properties. As these new technologies are perfected, the disk drives are doubling in capacity every six month while keeping the same footprint.

# # DISK HARDWARE

Workstation and personal computer disk drives have primarily been either Integrated Drive Electronics (IDE) drives or Small Computer System Interface (SCSI) drives. IDE drives integrate all the controller functions into the disk housing. SCSI drives also integrate controller functions in the disk assembly but require a more complex adapter