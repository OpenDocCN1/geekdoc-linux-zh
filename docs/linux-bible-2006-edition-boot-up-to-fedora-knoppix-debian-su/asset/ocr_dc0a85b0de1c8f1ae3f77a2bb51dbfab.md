# Chapter 24 ♦ Running Linux, Apache, MySQL, and PHP (LAMP) Server 649

In a LAMP server, MySQL is used for storing data appropriate to the Web applications that are being used. Common uses include data such as usernames and passwords, entries in a journal, and data files.

> > Note If you are not sure how a database works, refer to the sidebar “How MySQL Databases Structured” in this chapter.

MySQL was originally developed by Michael (Monty) Widenius of TcX (Sweden). In 1994, TcX released a backend database for Web applications and decided to use one supporting SQL, a standardized and widely recognized language for interacting with databases.

TcX investigated the free databases that were available at the time, plus some commercial databases, but could not find a system that supported the features it needed and could handle large databases at the same time. Because it already had experience writing database programs, TcX decided the best way to get what it wanted was to develop a new system that supported SQL.

In 1995, TcX released the source code for MySQL on the Internet. MySQL was not an open source program at that time (because of some of the restrictions in its license), but it still began to see widespread use. MySQL was later released under the GNU General Public License (GPL).

# PHP

PHP is a programming language that was developed specifically for use in Web scripts. It is preferred by many developers because it's designed to be embedded in HTML documents, making simpler to make Web content and scripts within a single file.

PHP originated as a set of Perl by Rasmus Lerdorf called PHP/FI (Personal Page/Forms Interpreter). Over time, more features were implemented, and Rasmus rewrote PHP/FI in C.

In 1997, Andi Gutmans and Zeev Suraski began working on a complete rewrite of PHP/FI. As the language evolved and more features were implemented, Gutmans and Suraski decided it would be appropriate to rename the project to accurately reflect these features. The name PHP Preprocessor (PHP) was chosen, with Lerdorf's approach, to maintain familiarity for users of PHP/FI.

The core features of PHP are included within the PHP code itself, and additional features are implemented in the form of extensions. On Debian, PHP is contained in the apache-mod-php4 package, and the extensions are stored in separate packages that can be installed at any time. Some of the most popular packages include:

+   * php-curl—This extension interfaces the CURL library, which contains interfaces for several types of servers, including LDAP, HTTP, and FTP.