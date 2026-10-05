
# Chapter 13 · Linux Database Software

![](img/cd7585e53abd949068548271c07fcdd8_201_0.png)

Figure 13–3 Results of the simple query from Figure 13-2.

## 13.2 Other Native Linux DBMSs

### Freeware

### PostgresSQL

Postgres has been around the UNIX world for quite some time. It is not purely relational and has some object-oriented features in its core. It's usually referred to as object-relational. In any event, in its most recent incarnation it supports nearly all of ANSI SQL plus some extensions, including embeddable functions. PostgreSQL also has APIs in C and Perl, Apache modules, and ODBC support. You can get more information from the PostgreSQL Web site: http://www.postgresql.org/

### Commercial

### Solid

Solid Technologies sells its DBMS for nearly every UNIX platform, including Linux for the x86 and Alpha architectures. Support for Solid is available for Python, Perl, PHP, and, of course, C.

This SQL server is aimed at higher-end applications and larger businesses. A free evaluation copy is available. Client software for non-Linux/UNIX systems is available, too. Solid supports a number of things you'd expect of a high-end server:

- On-line backups (i.e., the server remains running and a “snapshot” is saved)
- Crash and power failure recovery to last checkpoint
- Fine-grained access control (at a similar level to MySQL’s)
- Open Database Connectivity (ODBC)
- Automatic crash recovery
- Symmetric Multiprocessing (SMP)

Solid’s manuals are available on HTML. Solid is designed to require a minimal amount of administration. It is easy to set up and more runs itself. System requirements are minimal: a couple of Mb of disk space and a Mb of free RAM.

Pricing for Linux is considerably less than other systems. As of this writing, Solid Technologies is offering the desktop version (single-user, only UNIX socket connections) free for Linux.
Information on Solid can be found at http://www.solidtech.com.

### Empress

Empress is one of the first commercial databases for Linux. It is a relational database, like Sybase or Oracle. Empress supports these features (among others):

- Multimedia support
- Checkpointing and rollback
- BLOBs (Binary Large Objects)
- Shared libraries and a C API
- Interfaces for Tcl/Tk, Perl, and for FORTRAN (!)
- A GUI builder for quick building of graphical interfaces to Empress applications
- Two-phase commit
- A CGI pass-through for processing Empress HTML SQL (EHSQL). ESQL is embedded into a document and then parsed by the CGI and passed on to the client browser.

Personal Empress for Linux is available also. More information on Empress can be found at

```
http://www.empress.com/
```

### Texpress

KE Software is a Canadian company that makes an object-oriented (as opposed to relational) database, along with numerous support applications and modules. It supports relational, free text, and multimedia data types. Texpress also supports:

- Massive datasets
- Object-Oriented (OO) features including inheritance.
- Extensibility. You can define methods on objects in the database. Methods can be defined for data display, validation, assignment, and branch expression. This effectively lets you write stored procedures and then associate them with a particular object or class of objects.

Texpress's design actually favors more complicated queries, processing them as fast, if not faster, as simpler ones. It also supports massive datasets with ease. As database applications become more and more common complicated, these are important features to consider.

Texpress's object-oriented design typically means that data can be stored present in a more natural fashion, and it handles less structured data better than a relational database server.

More information on Texpress can be had at http://www.kesoft-software.com/.

### Essantia

Essantia is another database that incorporates some non-traditional technology. It employs what its developer, Intersoft, calls RISE, Reduced Instruction Set Engine. The communication interface is kept small and well-defined. It supports both relational- and object-oriented models of data management.

Essentia also supports these features:

- Journaling and consistency checking.
- Database versions—allows you to go back and examine previous states of databases.
- Incremental backups.
- Shadowing—data to be modified are copied to a shadow and not committed until a checkpoint is cleared.
- Locking at the row, table, and schema levels.

More information on Essentia and Intersoft is at http://www.intersoft.com/.

## 13.3 Other Databases with Partial Support

### Sybase

While there is no server for Linux, Sybase has made client libraries available for free. They’re somewhat dated and in a .out format, but if you need them they’re better than nothing.

### Oracle

While not supported by Oracle, it is possible to run the Santa Cruz Operation (SCO) version using Intel Binary Compatibility Specification (IBCS) compiled either as a module or into the kernel. However, Oracle is complicated and expensive. It’s likely that your substantial financial investment could be better spent on a database that has support for Linux such as Solid or Texpress.

## 13.4 Summary

As you’ve noticed, even if you only skimmed this chapter, Linux has a fairly large and rich set of databases available for use, ranging from the very lightweight MySQL to the freeway to large commercial database servers like Empress, Solid, and Texpress to Oracle running in SCO emulation.

All of these servers have different strengths and weaknesses. If you find that one of the smaller free or shareware database servers isn't fulfilling your needs, nearly every commercial server listed here offers free or low-cost personal editions and/or trial versions of their larger packages.

Take a few weeks to really evaluate these before shelling out what could be a substantial amount of money.

# Chapter 14 Programming Languages

So many languages, so little time.

Aside from everything else that Linux does, it provides some extraordinary programming languages to make repetitive tasks, or ones that don't seem easy to fix, very easy to fix.

The number of extant programming languages is quite large. There are literally scores, maybe hundreds, depending on how you choose to split a few hairs, and nearly all of the more popular ones, have at least one implementation under Linux. To attempt to give even a brief summary of all of them would be a small book. In this chapter we take a break from the most important ones: those that we use for. Still not understand why Object-Oriented Programming (OOP) is so cool and does Common Gateway Interface (CGI).

## 14.1 C

```
http://www.fsf.org/software/gcc/gcc.html
http://www.accu.org/
```

Neither of us are big programmers. We know enough to hack C a little and write small programs, but C is such an important language, in a UNIX-like system, it is rightly placed first. The kernel and most of the everyday commands you use are written in C. If you don't know C now, in the course of compiling and installing software, you will at least become familiar with it.

GCC is the "native" compiler for Linux. It supports everything a good compiler should: optimization, debugging, ANSI C support, POSIX compliance; and more than a lot of compilers that are shipped with or are available for some commercial OSs (SunOS 4 in particular had a very lame compiler, but it was enough to compile the first stage of gcc to bootstrap your way up to a full gcc compiler).

C is the most popular compiled language for high-performance general programming. Because it is compiled, it is typically faster than an interpreted language like Perl or Python. C is also a fairly low-level language. This type leads to longer development times for software. On the other hand, because it is a low-level language, it is possible to tune code to achieve very high performance.

Because C exists for virtually every OS and platform, it is usually possible to port a C program to other platforms. Architecture or OS-specific libraries obviously complicate this process (GUI libraries especially), but frequently angels on the target platform.

When it comes right down to C, C is the foundation for all the other languages discussed here in their compilers and/or interpreters were (some of the compiled languages compile their own compilers) written at nearly all of them offer high-level methods or functions for accomplishing various tasks, a proficient C programmer can write a program to do it as fast as if.

The reason people use higher-level (often interpreted) languages is that the development time for applications is typically much shorter, and for the smaller tasks often addressed by higher-level languages, the performance trade-off is more than acceptable. This is not to say that larger applications
