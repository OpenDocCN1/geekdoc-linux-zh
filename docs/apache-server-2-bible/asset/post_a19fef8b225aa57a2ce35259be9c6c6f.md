
## Part III: Running Web Applications

### Chapter 12: Running CGI Scripts

- What Is CGI?
- CGI Input and Output
  - GET requests
  - POST requests
  - Comparing GET and POST
  - Decoding input data
- Apache CGI Variables
  - Server variables
  - Client request variables
- Configuring Apache for CGI
  - Aliasing your CGI program directory
  - Choosing specific CGI file extensions
  - Enabling cgi-bin access for your users
  - Creating new CGI extensions by using AddType
- Running CGI Programs
  - Writing CGI Scripts in Perl
- Enabling CGI Debugging Support in Apache
  - ScriptLog
  - ScriptLogLength
  - ScriptLogBuffer
- Debugging Your Perl-Based CGI Scripts
  - Debugging from the command line
  - Debugging by using logging and debug printing
  - Debugging with CGI::Debug

### Chapter 13: Server Side Includes (SSI)

- What Is a Server Side Include?
- Configuring Apache for SSI
  - Enabling SSI for an entire directory
  - Enabling SSI for a specific file type
  - Using XBitHack for .htm or .html files
- Using SSI Commands
  - config
  - echo
  - exec
  - fsize
  - lastmod
  - include
  - printenv
  - set
- SSI Variables
- Flow Control Commands

### Chapter 14: Configuring Apache for FastCGI

- What Is FastCGI?
- Achieving high performance by using caching
- Scalability through distributed applications
- Understanding How FastCGI Works
  - Basic architecture of a FastCGI application
  - Different types of FastCGI applications
- Migrating from CGI to FastCGI
  - Things to keep in mind about migrating
  - Migrating a sample script
- Setting Up FastCGI for Apache
  - FastCGI directives for Apache
  - Configuring httpd.conf for FastCGI

### Chapter 15: PHP and Apache

- Understanding How PHP Works
- Bringing PHP to Your Company
- Prerequisites for PHP
- Compiling and Installing PHP
  - Building PHP as a CGI solution
  - Building PHP as an Apache module
- Configuring Apache for PHP
- Configuring PHP by Using php.ini
  - PHP directives in httpd.conf
  - PHP Directives directives in php.ini
- Working with PHP
  - Creating a simple command-line PHP script
  - Creating simple PHP Web pages
  - Using a PHP script as a Server-Side Include
  - Using a PHP page for a directory index
  - Using include files
  - Enhancing error handling with PHP
  - Processing Web forms with PHP
  - Creating sessions with PHP
  - Using MySQL with PHP
    - Creating a simple PHP page to access a MySQL database
    - Securing PHP include files
    - Authenticating users with PHP and MySQL

### Chapter 16: Using Perl with Apache

- Compiling and Installing mod_perl
- Running CGI Scripts by Using mod_perl
- Don’t Reinvent the Wheel
- Creating mod_perl Module by Using the Perl API for Apache
- Using CGI.pm to Write mod_perl Modules
- Preloading Perl Modules to Save Memory
- Keeping Track of mod_perl Modules in Memory
- Implementing ASP by Using the Apache:ASP Module

### Chapter 17: Running Java Servlets and JSP Pages with Tomcat

- Why Use Servlets?
- Installing Tomcat
  - Installing the latest JDK for Tomcat
  - Installing Tomcat and the mod_jk module
- Configuring Tomcat
  - Configuring Tomcat for Apache
  - Configuring Tomcat to use the Java Security Manager
- Configuring Apache for Servlets and JSP
- Working with Tomcat
  - Disabling Tomcat’s default HTTP service
  - Starting and stopping Tomcat
  - Starting Tomcat with a shell wrapper script
  - Running Java servlets

## Part IV: Securing Your Web Site

### Chapter 18: Web Security

- Understanding Web Security
- The Security Checkpoints
  - Checkpoint 1: Your network
  - Checkpoint 2: The operating system
  - Checkpoint 3: Web server software
