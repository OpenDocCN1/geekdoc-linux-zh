# TABLE 17.7 (CONTINUED) Web Resources for the Most Commonly Used Programming Languages, and UNIX Commands and Tools for Program Development

# General Pages: Shell Commands, Shell Programming, Advanced UNIX, and Program Development Tools

| capone.mtsu.edu/csdept/FacilitiesAndResources/make.htm | A small tutorial on the make utility |
| heather.cs.ucdavis.edu/~matloff/UnixAndC/CLanguage/Make.html | Very good tutorial on makefiles and libraries |

# gdb and GNU Tools for Software Testing

| http://www.gnu.org/software/gdb/gdb.html | The home page for gdb, the GNU project debugger |
| http://www.gnu.org/manual/ | Online documentation for GNU packages |

# Revision Control with Git/GitHub

| http://gitref.org/ | A comprehensive reference site for Git |
| http://git-scm.com/ | Open source site for Git hosted on GitHub |
| https://github.com/ | GitHub hosting site |
| en.wikipedia.org/wiki/GitHub | The Wikipedia site for GitHub |

+   - Splits the project development into multiple independent lines, called branches, which can evolve separately
+   - Regularly recombines branch content by merging, or reconciling, the content changes made in two or more branches
+   - Allows many people to work on a project simultaneously, sharing and combining their work as needed, at any convenient time

Git and GitHub are atomic-level, distributed, content-oriented version control systems. Atomic level means that when you take a snapshot of the software, everything in it is captured in the snapshot at a single instance in time. Distributed means that the entire software package you are working with is available to all collaborators locally at all times. Content oriented means that when you join different branches of work on the software, only the content of lines in the files along the branches you are merging are considered. Git indicates merged-content conflicts with several useful strategies and mechanisms, and resolves them using several tools that are add-ons to Git. But only the people writing, building, and testing how the software works, and those people managing that process, are responsible for resolving merged-context conflicts.

The purpose of the static analysis phase is to identify features of the software that might be bugs or nonportable, and to measure metrics such as lines of code (LOC), function points (FPs), and repetition count for functions. The UNIX tools that can be used for this purpose include lint, prof, and dprof.

The purpose of the dynamic analysis phase is to analyze programs during their execution. The tools used during this phase are meant to trace program execution in order to debug them and measure their run-time performance in terms of their execution time. The commonly used UNIX tools for this phase of the software life cycle are debuggers (gdb, etc.) and tools for measuring running times of programs (time).