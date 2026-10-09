| Topic | FastCGI Applications | mod_perl Scripts |
| --- | --- | --- |
| Database connectivity | Because all requests are sent to a single FastCGI application, you only need to maintain a single database connection with the back-end database server. However, this can change when Apache FastCGI process manager spawns additional FastCGI application instances because of heavy load. Still, the number of FastCGI instances of an application is likely to be less than the number of Apache child processes. | Because each Apache child process runs the `mod_perl` script, each child can potentially have a database connection to the back-end database. This means that you can end up with hundreds of database connections from even a single Apache server system. |

♦ ♦ ♦