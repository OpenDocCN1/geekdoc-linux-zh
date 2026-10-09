
**WAN**: Wide Area Networks used to connect distant sites, even on a continental scale

**WDM drivers**: Device drivers that adhere to the Windows Driver Model (WDM). WDM includes support for Windows 2000 power management, Plug and Play, and Windows Management Instrumentation (WMI). WDM is implemented on Windows 2000, Windows 98, and Windows Millenium Edition, so WDM drivers are source compatible between these operating systems and in many cases are also binary compatible. There are three types of WDM drivers: bus drivers, function drivers, and filter drivers.

**Win32 services**: A mechanism to start processes at system startup time that provide services not tied to an interactive user. Services are similar to UNIX daemon processes and often implement the server side of client/server applications.

**WMI (Windows Management Instrumentation)**: A component of the executive that enables device drivers to publish performance and configuration information and receive commands from the user-mode WMI service. Consumers of WMI information can be on the local machine or remoted across the network.

## B Annotated Reading List

This appendix contains an annotated reading list of books and papers of interest to builders and users of Beowulf clusters.

## C Annotated URLs

Below is a sampling of URLs that are helpful for those building or using a Beowulf. This is not an exhaustive list, and we encourage the reader to browse the Web for other sites. A good place to start is the general Beowulf Web sites.

### C.1 General Beowulf Information

- **www.beowulf.org:** The original Beowulf Web site.
- **beowulf-underground.org:** The Beowulf Underground provides “unsanctioned and unfettered information on building and using Beowulf systems.” It is a site that allows the Beowulf community to post brief articles about software, documentation, and announcements related to Beowulf computing. Each article includes links to Web sites and downloads for the various items. A separate commercial and vendor area keeps free software well delineated. Moderators work to keep the material brief and on topic and to prevent abuses. This is the one stop for all things Beowulf.

### C.2 Node and Network Hardware

- **www.cs.virginia.edu/stream:** The STREAM Benchmark provides a simple measure of the performance of the memory system on a node. This site also includes results for a wide variety of platforms, from PC nodes suitable for a Beowulf, to workstations, to supercomputers.
- **www.tomshardware.com:** Aimed at hobbyists building their own computers, this is a good site for general background on node hardware and includes up-to-date instructions on building your own node.

### C.3 Performance Tools

- **www.netlib.org/benchmark/hpl:** Home of the High Performance Linpack Benchmark

### C.4 Parallel Programming and Software

- **www.mpi-forum.org:** The official MPI Forum Web site, contains Postscript and HTML versions of the MPI-1 and MPI-2 Standards.
- **www.mcs.anl.gov/mpi:** A starting point for information about MPI, including libraries and tools that use MPI and papers about the implementation or use of MPI.
- **www.mcs.anl.gov/mpich:** Home of the MPICH implementation of MPI. Download source, documentation, and Unix and Windows versions of MPI from here. Also check the bug list page for patches and announcements of releases.
- **www.mcs.anl.gov/mpi/mptest:** Performance tests for MPI, including a guide for how not to measure communication performance.
- **www.netlib.org:** A valuable collection of mathematical software and related information.
- **www.csm.ornl.gov/pvm:** PVM home page.
- **www.mcs.anl.gov/romio:** Home of the ROMIO implementation of the I/O chapter from MPI-2. ROMIO is included in MPICH and LAM but can also be downloaded separately. Information on tuning ROMIO for performance can be found here.
- **hdf.ncsa.uiuc.edu:** Home of HDF. Included here are I/O libraries; tools for analyzing, visualizing, and converting scientific data; and software downloads, documentation, and support information.
- **www.cs.dartmouth.edu/pario:** Home of the Parallel I/O Archive. This includes a list of projects in parallel I/O, people working in parallel I/O, and conferences on parallel I/O. Its biggest claim to fame is an extensive annotated bibliography of parallel I/O resources.

### C.5 Scheduling and Management

- **www.openpbs.org:** The OpenPBS site is the official Web site for the open source version of PBS. Maintained by Veridian, it offers downloads of software, patches, and documentation, and it hosts FAQs, discussion lists, searchable archives, and general PBS community announcements.
- **www.pbspro.com:** Focused on the Professional Version of PBS, the PBS Pro Web site includes software downloads, documentation, evaluation versions, beta releases of new software, news, and information for the PBS administrator.
- **www.supercluster.org:** The Supercluster Web site contains documentation for the Maui scheduler and Sliver metascheduler. It also includes cluster-relevant research in areas of simulation, metaccheduling, data staging, allocation management, and resource optimization.

### C.6 Other

- **www.vrco.com:** VRCO provides virtual reality-based software including immersive environments for Windows 2000.
- **www.seattlelab.com:** Seattle Labs provides remote access tools for Windows 2000 including TelnetD and remote control tools.
- **www.citrix.com:** Citrix provides an extension to Window 2000 Terminal server that allows users from non-Windows platforms to remotely access Windows-based systems using the native Windows interface.
- **www.cs.cornell.edu/tech2000:** This web site describes the Intel funded Technology for Education 2000 project at Cornell University.
- **www.tc.cornell.edu:** This is the home page of the Cornell Theory Center (CTC), a high-performance cluster computing and interdisciplinary computational research center at Cornell University—home to the largest Windows/Intel/Dell cluster complex in the world.
- **www.tc.cornell.edu/AC3:** The Advanced Cluster Computing Consortium (AC3) at CTC—a consortium that includes computing manufacturers, software vendors, academies, government agencies, and corporate clients who focus on industry standard IT solutions that maximize the performance, reliability, and usability of Intel-based servers operating Windows 2000.
- **www.ctc-manhattan.com:** This is CTC’s cluster computing showcase and computational finance solutions center located at 55 Broad St. in Manhattan.

## References

Cray Research. Application Programmer's Library Reference Manual, 2nd edition, November 1995. Publication SR-2165.

Jack Dongarra. Performance of various computers using standard linear equations software. Technical Report Number CS-89-85, University of Tennessee, Knoxville TN, 37996, 2001. http://www.netlib.org/benchmark/performance.ps.

G. C. Fox, S. W. Otto, and A. J. G. Hey. Matrix algorithms on a hypercube I: Matrix multiplication. Parallel Computing, 4:17–31, 1987.

William Gropp, Steven Huss-Lederman, Andrew Lumsdaine, Ewing Lusk, Bill Nitzberg, William Schirp, and Marc Snir. MPI – The Complete Reference: Volume 2, The MPI-2 Extensions. MIT Press, Cambridge, MA, 1998.

William Gropp, Ewing Lusk, Nathanboss, and Anthony Skjellum. A high-performance, portable implementation of the MPI Message-Passing Interface standard. Parallel Computing, 22(6):789–828, 1996.

William Gropp, Ewing Lusk, and Anthony Skjellum. Using MPI: Portable Parallel Programming with the Message Passing Interface, 2nd edition. MIT Press, Cambridge, MA, 1999.

William Gropp, Ewing Lusk, and Rajeev Thakur. Using MPI-2: Advanced Features of the Message-Passing Interface. MIT Press, Cambridge, MA, 1999.

William D. Gropp and Ewing Lusk. Reproducible measurements of MPI performance characteristics. In Jack Dongarra, Emilio Luque, and Tomás Margalef, editors, Recent Advances in Parallel Virtual Machine and Message Passing Interface, volume 1697 of Lecture Notes in Computer Science, pages 11–18. Springer Verlag, 1999. 6th European PVM/MPI Users' Group Meeting, Barcelona, Spain, September 1999.

J. M. D. Hill, B. McCall, D. C. Stefanescu, M. W. Goudreau, K. Lang, S. B. Rao, T. Suel, T. Tsantilis, and R. H. Bisseling. BSPlib: The BSP programing library. Parallel Computing, 24(14):1947–1980, December 1998.

Message Passing Interface Forum. MPI: A Message-Passing Interface standard. International Journal of Supercomputer Applications, 8(3/4):165–414, 1994.

Message Passing Interface Forum. MPI2: A message passing interface standard. International Journal of High Performance Computing Applications, 12(1–2):1–299, 1998.

OpenMP Web page. www.openmp.org.

R. Reussner, P. Sanders, L. Prechelt, and M. Müller. SkaMPI: A detailed, accurate MPI benchmark. In Vasile Alexandrov and Jack Dongarra, editors, Recent advances in Parallel Virtual Machine and Message Passing Interface, volume 1497 of Lecture Notes in Computer Science, pages 52–59. Springer, 1998. 5th European PVM/MPI Users' Group Meeting.

Marc Snir, Steve W. Otto, Steven Huss-Lederman, David W. Walker, and Jack Dongarra. MPI – The Complete Reference: Volume 1, The MPI Core, 2nd edition. MIT Press, Cambridge, MA, 1998.

Rajeev Thakur, Ewing Lusk, and William Gropp. A case for using MPI’s derived datatypes to improve I/O performance. In Proceedings of SC98: High Performance Networking and Computing, November 1998.
