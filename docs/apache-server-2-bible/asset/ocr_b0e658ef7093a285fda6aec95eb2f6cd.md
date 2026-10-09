| Features | NDBM | SDBM | GDBM | BSD-DB |
|---|---|---|---|---|
| Creates FTP-safe files | No | Yes | Yes | Yes |
| Speed | Unknown | Slow | Medium | Fast |
| Database size | Unknown | Small | Large | Medium |
| Code size | Unknown | Small | Large | Large |
| Source comes with Perl | No | Yes | No | No |

This table is based on the information found in Perl 5 documentation. Before you can use any DBM with Apache, do this to make sure the DBM you choose is already installed in your system. Do this by confirming that the DBM library files are located in your system's default library directory. You are going to need Perl with DBM support. Make sure you have the latest version of Perl compiled with the chosen DBM support.

> You can download Perl from `www.perl.com`. Configuring Perl for DBM support is quite easy. Just run the configuration script, and it will prompt you for the DBM support. For example, if you choose `NDBM` or `GDBM` as your desired DBM, and if you have them installed on your system, the Perl configuration script should ask whether you want to compile Perl with `-ln dbm`, `-lgdbm`, and library flags.

After you have installed the appropriate DBM libraries on your system, you then need to configure Apache for support of DBM files, because the standard Apache distribution does not enable DBM support. Configure Apache source by using `--enable-auth-dbm` option with `configure` script, and by compiling and installing Apache as usual.

> If you have trouble compiling Apache, try adding the `-lyour_dbmaname` to `EXTRA_LIBS` in the `configuration` file. For example, if you are using GDBM, you can add `-lgdbm` so that `EXTRA_LIBS=-lgdbm`. Make sure you rerun the `configure` script and run `make` again afterwards. In case of problems, it might be best to try GNU GDBM because it is heavily used by many different systems and you are likely to get help in USENET newsgroups.

After Apache is properly compiled for DBM files, you can use dbmmanage to create a DBM user file. Begin by using the dbmmanage Perl script found in the support directory of the standard Apache distribution (or the source distribution) for creating a DBM-based user file. The dbmmanage Perl script can create many popular DBM files such as NDBM, GDBM, and Berkeley DB files. This script can be used to create a new DBM file, to add users and passwords, to change passwords, to delete users, or to view user information. Before using the script, you should modify the following line in the script so that the DBM you want to use is listed as the first item in the ISA array:

```
BEGIN { @AnyDBM_File::ISA = qw(DB_File, NDBM_File, GDBM_file) }
```