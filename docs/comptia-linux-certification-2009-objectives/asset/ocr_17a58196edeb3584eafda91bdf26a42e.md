# Apache Modules

Apache has a set of compiled modules that extend its core functionality. The modules can be integrated with Apache as add-ons.

| **Module** | **Description** |
| :--- | :--- |
| mod_access | Used for restricting access to clients, based on the client request that involves the characteristics such as the client hostname and IP address. |
| mod_ssl | Used for providing a secure support for the Apache server using the Securer Socket Layer (SSL) and Transport Layer Security (TLS) protocols. |
| mod_php | Used for recognizing PHP scripts. |
| mod_spelling | Used for correcting URLs written with any capitalization issues and misspelling issues. |
| mod_perl | Used for recognizing Perl scripts. |
| mod_cgi | Used for recognizing Common Gateway Interface (CGI) scripts. |

![](bbox=[0.76, 0.09, 0.87, 0.175])

# Hypertext Preprocessor (PHP)

Hypertext Preprocessor (PHP) is an open source scripting language that is used to create dynamic web pages. PHP is a server-side scripting language, and so scripts written in PHP are executed on the server and the client will not be able to view the code. PHP is compatible with any type of database.

The php.ini configuration file controls the behavior of PHP in Linux. By default, PHP looks for the file in the current working directory, using the path specified by the environment variable PHPRC or the path specified while compiling. It has various functions, for example, it can be used to change the severity of errors that need to be logged.

# Apache Configuration Directives

There are a set of directives defined in the Apache distribution. Each directive is set to specific values and defines specific formats. Some of the frequently used directives are listed in the table.

| **Directive** | **Description** |
| :--- | :--- |
| ServerAdmin | Specifies the email address that is used in error messages sent to a client. |
| CustomLog<br>LogFormat | Specifies the log file name and the log format. Describes the format of the access log files. It defines either of the two forms; the form that uses a single argument, which specifies the explicit format or the form that uses a nickname to define the explicit format. |

![](bbox=[0.76, 0.65, 0.87, 0.74])