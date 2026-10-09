Like `mod_perl` scripts, FastCGI applications run all the time (after the initial loading) and therefore provide a significant performance advantage over CGI scripts. Table 22-3 explains the differences between a FastCGI application and a `mod_perl` script.

![](bbox=[0.12, 0.22, 0.21, 0.29])

To learn more about FastCGI, see Chapter 14.

**Table 22-3**
**Difference Between a FastCGI Application and `mod_perl` Scripts**

| Topic | FastCGI Applications | `mod_perl` Scripts |
| :--- | :--- | :--- |
| Apache platform dependent | No. FastCGI applications can run on non-Apache Web servers such as IIS, Netscape Web Server, and the like. | Yes. Only Apache supports `mod_perl` module. |
| Perl only solution | No. FastCGI applications can be development in many languages including C, C++, and Perl. | Yes |
| Runs as external process | Yes | No |
| Can run on remote machine | Yes | No |
| Multiple instances of the application/script are run | Typically, a single FastCGI application is run to respond to many requests that are queued. However, if the load is high, multiple instances of the same application are run. | Number of instances of `mod_perl` script that run is equal to the number of child Apache server processes. |
| Wide support available | Yes. However, I sometimes get the impression that FastCGI development is slowing down but I can't verify this or back this up. | Yes. There are a great deal of `mod_perl` sites on the Internet and support via Usenet or Web is available. |