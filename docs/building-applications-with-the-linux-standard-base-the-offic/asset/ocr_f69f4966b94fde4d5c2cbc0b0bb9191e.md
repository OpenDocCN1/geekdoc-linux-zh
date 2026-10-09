use a license allowing the LSB team to redistribute them along with the other test tools. To be considered for inclusion in appbat, an application also had to be fairly close to complete adherence to the LSB Written Specification. This means it could not use any non-LSB APIs from the LSB shared libraries, and only use a minimal number of non-LSB shared libraries.

For the initial LSB v1.2 Certification program, appbat only consisted of four applications, of which only two needed to be tested. When the LSB v1.3 Certification program began, the number of applications increased to eleven for the Intel 32-bit architecture, eight for the Itanium architecture, and ten for the PowerPC 32-bit architecture. An additional requirement for LSB v1.3 is that all LSB Certification Ready applications in appbat must be used when certifying an LSB Runtime Environment. An application is considered LSB Certification Ready when it has met all the requirements for LSB Application certification, including things like passing the LSB application checker, executing properly in the LSB Sample Implementation, and executing properly in two different LSB Certified Runtime Environments. Here is a list of the eleven applications in appbat for the LSB v2.0 Certification program for all supported processor architectures:

+   - Apache—Web server
+   - Celestia—visual space simulation
+   - expect—application that “talks” to other programs
+   - groff—document formatting system
+   - Lynx—text-based Web browser
+   - Python—interpreted, interactive, object-oriented programming language
+   - rsync—program for synchronizing files over a network
+   - Samba—file and print server for SMB/CIFS clients
+   - Tcl—embedded scripting language
+   - XPaint—paint program for the X Window System
+   - xpdf—PDF file viewer for the X Window System