+   - deb-pkg - Build the kernel as an deb package
+   - tar-pkg - Build the kernel as an uncompressed tarball
+   - targz-pkg - Build the kernel as a gzip compressed tarball
+   - tarbz2-pkg - Build the kernel as a bzip2 compressed tarball

Documentation targets:

+   - man - Linux kernel internal documentation in different formats:
+     - xmldocs (XML DoCbook), pedocs (Postscript/PDF), pdfdocs (PDF)
+     - htmldocs (HTM), man docs (pages, use installmandocs to install)

Architecture specific targets (arm):

+   - zImage - Compressed kernel image (arch/arm/boot/zImage)
+   - Image - Uncompressed kernel image (arch/arm/boot/Image)
+   - xipImage - XIP kernel image, if configured (arch/arm/boot/xipImage)
+   - bootpImage - Combined zImage and initial RAM disk

+   - install - Install initrd image via make variable INITRD=<path>
+   - zinstall - Install uncompressed kernel
+   - install - Install compressed kernel
+     - Install using (your) ~/bin/installkernel or
+     - (distribution) /sbin/installkernel or
+     - Install to $(INSTALL_PATH) and run lilo

+   - assabet_defconfig - Build for assabet
+   - badge4_defconfig - Build for badge4
+   - bast_defconfig - Build for bast
+   - cerfcube_defconfig - Build for cerfcube
+   - clips7500_defconfig - Build for clips7500
+   - colli_defconfig - Build for colli
+   - corgi_defconfig - Build for corgi
+   - ebsa110_defconfig - Build for ebsa110
+   - edb7211_defconfig - Build for edb7211
+   - emx2611_defconfig - Build for emx2611
+   - ep80219_defconfig - Build for ep80219
+   - epax10d_h_defconfig - Build for epax10dH
+   - foodbridge_defconfig - Build for foodbridge
+   - fortunet_defconfig - Build for fortunet
+   - h3600_defconfig - Build for h3600
+   - h7201_defconfig - Build for h7201
+   - h7202_defconfig - Build for h7202
+   - hackkit_defconfig - Build for hackkit
+   - integrator_defconfig - Build for integrator
+   - igi1244_defconfig - Build for igi1244
+   - iq80321_defconfig - Build for iq80321
+   - iq80331_defconfig - Build for iq80331
+   - iq80332_defconfig - Build for iq80332
+   - ixdp2400_defconfig - Build for ixdp2400
+   - ixdp2401_defconfig - Build for ixdp2401
+   - ixdp2800_defconfig - Build for ixdp2800
+   - ixdp2801_defconfig - Build for ixdp2801
+   - ixp4xx_defconfig - Build for ixp4xx
+   - Jornada720_defconfig - Build for jornada720
+   - lart_defconfig - Build for lart
+   - lpd7a400_defconfig - Build for lpd7a400
+   - lpd7a404_defconfig - Build for lpd7a404
+   - lubbock_defconfig - Build for lubbock