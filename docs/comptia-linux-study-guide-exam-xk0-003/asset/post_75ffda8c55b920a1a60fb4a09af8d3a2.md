
## Exam Essentials

**Identify critical features of RPM and Debian package formats.**
RPM and Debian packages store all files for a given package in a single file that also includes information on what other packages the software depends on. These systems maintain a database of installed packages and their associated files and dependencies.

**Describe the process of installing an RPM or Debian package.**
Use the rpm program or Yum to install an RPM package, or use dpkg or apt-get to install a Debian package. These programs install, upgrade, or remove all files associated with a package and maintain the associated databases.

**Summarize methods of working around package dependency problems.**
Dependency problems can be overcome by forcing an installation, upgrading or installing the depended-on package, recompiling the package, or installing another version of the target package. Which approach is best depends on the specifics of the system involved.

**Describe how to install a program from a source code tarball.**
Compiling a program from source code depends greatly on the program in question. Most provide a configuration script called configure or a configure target in the Makefile. Once that’s run, you type make to build the package and then install it with an install script or an install target in the Makefile.

**Summarize backup hardware options.**
Backup hardware includes tapes, dedicated hard disks, removable disks, and optical media. Tapes have been the most common type of backup hardware in the past, but each of the others has its place for particular backup types, and hard disks have dropped in price enough to make them appealing as an everyday backup medium.

**Describe how Linux writes to optical media.**
Linux uses the mkisofs program to create an ISO-9660 filesystem (and optionally other common optical disc filesystems), which is then burned to the disc by cdrecord. These programs may be piped together, and common GUI front-ends can help in this process by providing a friendlier user interface.

## Review Questions

1. You are installing a small program from source code and need to change a number of options. You cannot find a specific configuration script for the program. In this case, what file should you edit?
   - A. configfile
   - B. change
   - C. make
   - D. makefile

2. Which of the following is not an advantage of a source package over a binary package?
   - A. A single source package can be used on multiple CPU architectures.
   - B. By recompiling a source package, you can sometimes work around library incompatibilities.
   - C. You can modify the code in a source package, altering the behavior of a program.
   - D. Source packages can be installed more quickly than binary packages can.

3. Which is true of using both RPM and Debian package management systems on one computer?
   - A. It's generally inadvisable because the two systems don't share installed file database information.
   - B. It's impossible because their installed file databases conflict with one another.
   - C. It causes no problems if you install important libraries once in each format.
   - D. It's a common practice on Red Hat and Debian systems.

4. Which of the following statements is true about binary RPM packages that are built for a particular distribution?
   - A. They can often be used on another RPM-based distribution for the same CPU architecture, but this isn't guaranteed.
   - B. They may be used in another RPM-based distribution only when you set the `--convert-distrib` parameter to `rpm`.
   - C. They may be used in another RPM-based distribution only after you convert the package with `alien`.
   - D. They can be recompiled for an RPM-based distribution running on another type of CPU.

5. Which is true of source RPM packages?
   - A. They consist of three files: an original source tarball, a patch file of changes, and a PGP signature indicating the authenticity of the package.
   - B. They require programming knowledge to rebuild.
   - C. They can sometimes be used to work around dependency problems with a binary package.
   - D. They are necessary to compile software for RPM-based distributions.

6. Which of the following do RPM filenames conventionally include?
   - A. Single-letter codes indicating Red Hat-certified build sites
   - B. Build date information
   - C. Version number and CPU architecture information
   - D. A CRC code for the package's contents

7. To use `dpkg` to remove a package called `thepprogram`, including its configuration files, which of the following commands would you type?
   - A. `dpkg -P thepprogram`
   - B. `dpkg -p thepprogram`
   - C. `dpkg -r thepprogram`
   - D. `dpkg -r thepprogram-1.2.3-4.deb`

8. Which of the following describes a difference between `apt-get` and `dpkg`?
   - A. `apt-get` provides a GUI interface to Debian package management; `dpkg` does not.
   - B. `apt-get` can install tarballs in addition to Debian packages; `dpkg` cannot.
   - C. `apt-get` can automatically retrieve and update programs from Internet sites; `dpkg` cannot.
   - D. `apt-get` is provided only with the original Debian distribution, but `dpkg` comes with Debian and its derivatives.

9. Which of the following is true of an attempt to use a Debian package from one distribution on another Debian-derived distribution?
   - A. It's unlikely to work because of library incompatibilities and divergent package-naming conventions.
   - B. It's guaranteed to work because of Debian's strong package definition and enforcement of standards for startup scripts and file locations.
   - C. It will work only when the distributions are built for different CPUs or when the `alien` package is already installed on the target system.
   - D. It's likely to work because of the close relationship of Debian-based distributions, assuming the two distributions are for the same CPU architecture.

10. The `tar` program may be used to complete which of the following tasks? (Choose all that apply.)
   - A. Install RPM and Debian packages.
   - B. Install software from binary tarballs.
   - C. Back up a computer to tape.
   - D. Create source code archive files.

11. The `tar` program provides a much easier ________ process than RPM and Debian package tools do.
   - A. dependency tracking
   - B. source code compilation
   - C. file ownership setting
   - D. package creation

12. What is wrong with the following commands, which are intended to record an incremental backup on a tape that already holds one incremental backup?

   ```bash
   # mt -f /dev/st0 fsf 1
   # tar cvlpf /dev/st0 --listed-incremental /root/inc /home
   ```

   - A. The `mt` command should terminate in 2, rather than 1, to skip to the second position on the tape.
   - B. When backing up /home, the incremental file must reside in /home, not in /root.
   - C. The device filename should be a nonrewinding name (such as /dev/nst0), not a rewinding name (/dev/st0).
   - D. The incremental backup must include the root (\/) directory; it cannot include only /home.

13. What is an advantage of using `rsync` for network backups, as compared to FTP or NFS?
   - A. `rsync` can be used by any user.
   - B. `rsync` can reduce network bandwidth use.
   - C. `rsync` can back up across architectures (x86 to PowerPC, for instance).
   - D. `rsync` can back up from any filesystem type (XFS, ReiserFS, and so on).

14. Which of the following is a true statement concerning the ability to restore a backup made using Linux's `dump` to a partition that's formatted with XFS?
   - A. You must use `cpio`'s -H `dump` option to do the job.
   - B. You must use the `dump` utility's -r option to do the job.
   - C. You must use the `xfsrestore` utility to do the job.
   - D. This task cannot be directly and easily performed.

15. You need to restore some files that were accidentally deleted. Which of the following commands can be used to list the contents of an archive stored on a SCSI tape?
   - A. `cpio -itv > /dev/st0`
   - B. `cpio -otv > /dev/st0`
   - C. `cpio -otv < /dev/st0`
   - D. `cpio -itv < /dev/st0`
