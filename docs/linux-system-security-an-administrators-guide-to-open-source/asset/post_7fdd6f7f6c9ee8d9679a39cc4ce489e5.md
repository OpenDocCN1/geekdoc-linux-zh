
**check_group**. Cross-references the group file looking for duplicate GIDs and groupnames, malformed entries, and inconsistencies that are probably the result of misconfiguration but should be investigated and corrected. This should run quickly.

**check_inetd**. The check_inetd script is designed to cross-reference the inetd.conf file with the services file, check the ownership and permissions of files referenced therein, verify that the files indicated in inetd.conf do exist and that they refer to the path expected. tiger tries to verify that the services are running on the expected port and that no vulnerable services are enabled. In order to perform these checks, tiger will attempt to compare the files on your system to files in the tiger_systems subdirectory. The script may not run to the best of its ability if the files for your particular system are not available. Note that you will need to modify this script if you are using xinetd.

**check_known**. check_known searches for known signs of intrusion. It looks for the presence of directories where normally plain files are expected and reports files in directories commonly used by intruders to hide files. It also searches for filenames that have been used by intruders in the past. The run time for this is usually short.

**check_netrc**. The .netrc file is used by FTP programs to store login and password information. The check_netrc script examines .netrc files and will report nonanonymous login information if found and if readable by others. It also looks for .netrc files that are symbolic links or directories (as both are unexpected). Example 13-7 shows a run of check_netrc.

# Example 13-7 Running the check_netrc Script

```
# scripts/check_netrc
Configuring... 

Will try to check using config for 'i686' running Linux 2.0.36...
--CONFIG-- (con005c) Using configuration files for Linux 2.0.36. Using 
configuration files for generic Linux 2.
Not all checks may be performed.
# Performing check of .netrc files...

# Checking accounts from /etc/passwd...
--WARN-- [rc002w] User bob's .netrc file contains passwords for 
non-anonymous ftp accounts.
```

**check_nisplus**. This script attempts to check the permissions are correctly set on NIS+ password entries. It can only be run stand-alone, unless you modify the main tiger script to run it.

**check_passwd**. The check_passwd script looks for possible misconfigurations or signs of compromise by reporting duplicate UIDs and usernames in the password file, as well as malformed password entries and conflicts between files on your system (such as passwd and shadow). This should run fairly quickly. Sample output from check_passwd is shown in Example 13-8.

# Example 13-8 Running check_passwd

```
# scripts/check_passwd
Configuring...
Will try to check using config for 'i686' running Linux 2.0.36...
--CONFIG-- [cono05C] Using configuration files for Linux 2.0.36. Using configuration files for generic Linux 2.
Not all checks may be performed.
# Performing check of passwd files...
--WARN-- [pass002w] UID 0 exists multiple times in /etc/passwd.
```

**check_path**. This script examines the path of root or all users (according to variables set in the tigerc file; see Table 13.6 on page 352) and reports directories that are writable by others, not owned by system users or the user being checked. It also looks for the presence of "." in the path, all of which can lead to execution of a Trojan horse program.

**check_perms**. This script examines the permissions of files and devices and reports any that have more accessibility than they should (world readable, or group writeable, for example). This script depends on availability of a system-specific file (file_access_list) in the systems subtype directory and may not run if a full port has not been done for your particular type and version of operating system.

**check_printcap**. The printcap file, used for printer control, may contain references to filters that may be run when a job prints. The check_printcap script evaluates the ownership and permissions of the files and directories associated with printer control and reports vulnerabilities. Execution of a vulnerable filter could result in unauthorized access.

**check_rhosts**. This script examines user .rhosts files and the hosts.equiv file for vulnerabilities and misconfigurations. Presence of `+`, `*` or an entry containing a host but no user (both of which could lead to unauthenticated connections) is reported, as are files with extra permissions which could allow someone to modify the file or gain information useful in compromising an account. The script verifies that there are no unusual characters present in the files and checks for .rhosts that are symbolic links or directories (both unexpected under normal circumstances). A policy configuration option enables you to allow certain local hosts to be present in users' .rhosts files but to report unapproved hosts (refer to Table 13.6 on page 352). Sample output from check_rhosts was shown in Example 13-4 on page 361.

**check_sendmail**. The check_sendmail script is dated, but it was designed to look for versions of sendmail that are old and likely to contain security holes. If it finds you are using the smcrsh (sendmail restricted shell) to control which programs may be executed by sendmail program aliases, it will check to see if your smrsh configuration allows potentially dangerous scripts to be run. smrsh is part of the sendmail distribution; for more information, see the sendmail documentation cited in sendmail Resources on page 379. Example 13-6 on page 363 shows output from check_sendmail.

**check_signatures.** Each of the files or binaries on your system can be fingerprinted with a cryptographic hash, or signature. The check_signatures script compares the cryptographic hash of each of the binaries and important files on your system against a set of cryptographic hashes stored in a database used by tiger. The database is created from files in the original OS distribution and may also contain cryptographic hashes of binaries distributed as patches to the operating system or binaries that are known to be compromised. These checks should be considered supplemental to tripwire (see Chapter 14).

Databases of signatures for several OS distributions are distributed with tiger. Updates are made available occasionally at the tiger FTP site, or you can try your hand at generating your own (see Modifying tiger on page 375 for more information). By running check_signatures against a good database, you can find out if any of the executables on your system have changed from the distribution, which is usually a sign of an intrusion. When you apply patches or new software to your system, you can add updates to your database of signatures.

**check_system.** Occasionally, there may be a check that is specific to a particular OS or flavor of that OS that you don't want to run on every system. check_system executes a prescribed list of scripts written specifically for the host operating system. There is a tigercc option to enable or disable running of the system-specific scripts (see Table 13.6 on page 352); if enabled, all system-specific checks will be run. For more information on check_system, see Modifying tiger on page 375.

**crack_run.** If you have configured Crack on your system (discussed in Chapter 12), you can ask tiger to run Crack as part of your regular tiger routines. See Running Crack from tiger on page 373 for details on configuration. Sample output from run_crack is shown in Example 13-9.

# Example 13-9 Running the run_crack Script

```
# scripts/crack_run
Configuring...

Will try to check using config for 'i686' running Linux 2.0.36...
--CONFIG-- [conf05C] Using configuration files for Linux 2.0.36. Using
configuration files for generic Linux 2.
Not all checks may be performed.

# Running Crack on password files...
(c) Alec Muffett, 1991, 1992, 1993, 1994, 1995, 1996
System: Linux topcat 2.0.36 #1 Tue Oct 13 22:17:11 EDT 1996 i686 unknown
Home: /usr/local/src/crack/c50a
Invoked: /usr/local/src/crack/c50a/Crack /usr/local/src/crack/c50a/run/tmp.pass
Stamp: linux-2-unknown

Crack: making utilities in run/bin/linux-2-unknown
find . -name '*'"-print | xargs -n50 rm -f'
( cd src; for dir in * ; do ( cd $dir ; make clean ) ; done )
make[1]: Entering directory `/usr/local/src/crack/c50a/src/lib'
```
