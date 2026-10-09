
- **Portable across major OS platforms** — PHP runs on all major platforms including Unix, Linux, Windows, OS/2, and Mac OS.
- **Portable across major Web server platforms** — In PHP 4.0, the Web server interface (Server API, or SAPI) is abstracted, which allows it to integrate well with different Web servers including Apache, IIS, IPanet/Netscape Enterprise Server, and Zeus.
- **Built-in support for major databases** — PHP implements native interfaces for all major databases, including MySQL, Postgres, Oracle, DB2, and MS SQL Server, which makes it a good candidate for database-driven Web development.
- **High performance** — PHP 4 was revamped for high performance; it is many times faster than PHP 3. A free add-on module called the Zend Optimizer from Zend Technologies can optimize an application to be 40 to 100 times faster than one that is not optimized. Many large Web sites are using PHP; you can learn about them at the PHP Web site at www.php.net.
- **Easy to learn for new developers** — PHP is a C-like language with automatic memory management (that is, no pointers to worry about). PHP also has elements of Perl, Java, and C++. Someone who knows any of these major languages can learn PHP in a matter of hours to days.
- **Supports Internet standards** — Internet standards, including IMAP, FTP, POP, XML, W3DX, LDAP, NIS, and SNMP, are supported. This means that PHP can interface with different standards and technologies with ease—all from one common tool set, without the need for expensive third-party modules.
- **Enterprise friendly** — Many large enterprises have bought into the Java platform already and many Java evangelists in such companies often find ways of making Java the “ideal” platform for even the smallest project, which often results in lengthy development cycles. Such companies are often ready to say no to everything else by stating that other core business logic has been already implemented in Java and therefore there is no room for PHP or its kind. Now you can say, not so fast! PHP 4 supports direct access to Java objects on any system that has Java Virtual Machines. It even supports Distributed COM (DCOM) on a Windows platform. PHP is becoming aggressive about integrating with Java and other enterprise technologies so that it can become hard to say no to PHP.
- **Open source community** — Open-source has proven to be a very effective software development approach. As an open-source project of the Apache Group, PHP enjoys the benefits of this approach. The PHP core developers participate in many open-source support forums such as Usenet news groups and IRC channels. Commercial support is also available from many Web software consulting companies.

## Prerequisites for PHP

Most sites using PHP also use MySQL as the database. If you plan to use MySQL, you should download the MySQL source or binary distribution from www.mysql.com/downloads/index.html. Read the installation documentation to learn how to install MySQL on your system. You also need the MySQL development packages. Covering MySQL installation for all the platforms is beyond the scope of this book.

On my Linux system running Apache, I have installed:

- The server RPM for i386 systems
- Client programs RPM for i386 systems
- Include files and libraries RPM for development for i386 systems
- Client shared libraries RPM for i386 systems

The include files and libraries are needed for PHP if you want to compile it with MySQL support.

# Compiling and Installing PHP

The current version of PHP is 4.0. You can download PHP source or binary distributions from `www.php.net`. This section assumes that you have downloaded the latest source distribution of PHP, `php-4.1.0.tar.gz`.

> If you are on Windows platform, read the Running PHP Scripts in Chapter 21 to install PHP for Apache.

After downloading the source distribution, extract the source in a directory by using the `tar xvzf php-4.1.0.tar.gz` command. I recommend that you install it in the same directory as you installed the Apache source. For example, if you installed Apache source in `/usr/local/src/httpd-2.0.16` directory, then extract PHP into the `/usr/local/src` directory. A new subdirectory, called `php-4.1.0`, will be created.

At this point, you have to decide how you plan to run PHP. PHP can be run as an Apache module (embedded in the server itself or as a DSO module) or as a CGI solution. The CGI solution means that you will not have any performance advantage over regular CGI scripts with PHP scripts because a PHP interpreter will be loaded each time to process a CGI-mode PHP script.

## Building PHP as a CGI solution

Like Perl, PHP can be used in standalone scripts as well as embedded in Web pages. To build the PHP interpreter for CGI-mode operations, do the following:

1. As root change to the PHP source distribution directory and run:
   `./configure --enable-docs-path`
2. Now run `make && make install` to compile and install the PHP interpreter on your system.

## Building PHP as an Apache module

You can either store the PHP module within the Apache binary or install it as a DSO module for Apache. An advantage of a DSO module is that it can be unloaded by just commenting out a configuration line in `httpd.conf`, thus saving some memory.

### Building PHP as a static Apache module

I assume that you have installed Apache source in `/usr/local/src/httpd-version` and PHP source in `/usr/local/src/php-version` directories. Here is how to compile and install PHP as a static Apache module:

1. If you have not yet installed Apache, run the following command as root from the Apache source distribution directory:

   ```
   ../configure --prefix=/usr/local/web/apache
   ```
   
   You can add other options if you wish to use them. Run `./configure --help` to determine whether any other option is suitable for your needs.

2. Now from the PHP source distribution directory run:

   ```
   ./configure --with-apache=../httpd-version \
   --with-mysql=/usr
   ```
   
   Here the `--with-mysql` option is set to `/usr` because MySQL RPM packages install the include files in `/usr/include/mysql` directory. If your system has MySQL includes in a different location, you should use a different directory name. You can discover where MySQL includes are kept by using the `locate mysql.h` command, which is available on most Unix systems with the locate database feature.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_455_0.png)

You do not need the `--with-mysql` option if you do not plan on using MySQL with PHP or want to use PHP's built-in support for MySQL, which is only recommended if you do not plan on using MySQL with `mod_perl` or other Apache modules.

3. Run the `cp php.ini-dist /usr/local/lib/php.ini` command to copy the `php.ini-dist` file to `/usr/local/lib` as `php.ini`. This is the PHP configuration file that is discussed later in the "Configuring PHP By Using php.ini" section.
4. Run `make && make install` to compile and install the PHP side of the source code.
5. Now change directory to the Apache source distribution and run:

   ```
   ./configure --prefix=/usr/local/apache
   --activate-module=modules/php4/libphp4.a
   ```
   
   You can add any other options in the above command-line. Run the `./configure --help` command for information about other options.

6. Run `make && make install` to compile and install Apache with PHP support.
7. Run the `/usr/local/apache/bin/apachectl restart` command to restart (or start) Apache.

# Building PHP as a Dynamic Shared Object (DSO) module

You must have DSO support enabled in Apache before you can use PHP as a DSO module. To recompile Apache with DSO support, do the following:

1. From the Apache source distribution directory run the following command as root:

   ```
   ./configure --prefix=/usr/local/apache --enable-so
   ```
   
   You can also add other options as necessary.

2. You can compile and install Apache using `make && make install` command.

After you have a DSO support-enabled Apache server, you can do the following to create a DSO module for PHP:

1. From the PHP source distribution directory run the following command as root:

   ```
   ./configure --with-apxs2=/usr/local/apache/bin/apxs \
       --with-mysql=/usr
   ```
   
   Here the `--with-mysql` option is set to `/usr` because MySQL RPM packages install the include files in `/usr/include/mysql` directory. If your system has MySQL includes in a different location, you should use a different directory name. You can find out where MySQL includes are kept by using the `locate mysql.h` command, which is available on most Unix systems with the locate database feature.

2. Now run `make && make install` to compile and install the DSO version of PHP module for Apache.
3. Run the `/usr/local/apache/bin/apachectl restart` command to restart (or start) Apache.

# Configuring Apache for PHP

After you have installed the `mod_php` module for Apache and configured `php.ini` as discussed earlier, you are ready to configure Apache for PHP as follows:

1. If you have compiled and installed PHP as a DSO module for Apache, add the following line to `httpd.conf` file:

   ```
   LoadModule php4_module    modules/libphp4.so
   ```

2. Add the following lines to the `httpd.conf` file

   ```
   <Files *.php>
     SetOutputFilter  PHP
     SetInputFilter   PHP
   </Files>
   ```
   
   This tells Apache that any file with `.php` extension must be treated as PHP scripts and should be processed using PHP input and output filters.
