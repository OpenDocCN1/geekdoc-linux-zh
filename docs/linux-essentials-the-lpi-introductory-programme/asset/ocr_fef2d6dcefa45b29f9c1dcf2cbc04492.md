# Table 2.1: Comparison of the most important Linux distributions (as of February, 2012):

| | RHEL | Fedora | SLES | openSUSE | Debian | Ubuntu |
|---|---|---|---|---|---|---|
| Supplier | Red Hat | Red Hat + Comm. | SUSE | SUSE/Comm. + Comm. | Debian Project | Canonical +Comm. |
| Target | Enterp. | Geeks | Enterp. | Private | Ent/Priv | Ent/Priv |
| Fees due? | yes | no | Support | no | no | no |
| First pub | 2003 | 2003 | 2000 | 2006 | 1993 | 2004 |
| Rel cycle | 3-4 yrs | ≈ 6 mth. | 3-4 yrs | 8 months | ≈ 2 yrs | 6 mth |
| Life cyc | 10 yrs | ≈ 1 yr | 7 yrs. | 18 months | 3-4 yrs | 5 yrs (LTS) |
| Platforms | 6 | 2 | 5 | 2 | 10 | 3 |
| Pkges (appr.) | 3000 | 26,000 | ? | 14,650 | 29,050 | 37,000 |
| Pkg format | rpm | rpm | rpm | rpm | deb | deb |
| Live media? | ? | yes | no | yes | yes | yes |

Both approaches include the comprehensive management of "dependencies" between software packages, which helps ensure the consistency of the system and to prevent the removal of software packages that other packages in the system rely on (or, conversely, to enforce their installation if another package being installed requires them and they are not installed already).

While users of Windows and OS X are used to obtaining software from a variety of sources<sup>7</sup>, at least the large distributions like Debian, openSUSE, or Ubuntu attempt to provide their users with a very comprehensive selection of software directly via the package administration tools. These allow access to the distributions' "repositories" and offer search functions (of varying quality) for particular software packages which can then be conveniently installed, possibly together with their dependencies, over the network.

It is important to note that it is not necessarily possible to exchange packages between distributions, even if these use the same basic packaging format (deb or rpm) — the packages contain various assumptions on how a distribution is put together which by far exceed the packaging format. It is not completely infeasible (Debian GNU/Linux and Ubuntu, for example, are similar enough that under the right circumstances it may be quite possible to install a Debian package on an Ubuntu system or vice-versa) but, as a rule of thumb, the deeper a package is rooted inside the system, the larger the chance of trouble occurring — a package that just contains a few executables and their documentation is likely to present fewer problems than a system service that must be integrated into the machine's startup sequence. If in doubt, refrain from experiments with an uncertain outcome.

Table 2.1 shows an overview of the most important Linux distributions. For more information, consult DistroWatch or the individual distributions' web sites.

> <sup>7</sup> However, Apple and Microsoft are now eager to establish the centralised "app store" concept known from smartphones for their PC operating systems, too.