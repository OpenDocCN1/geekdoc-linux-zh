CGI.pm module. This makes Perl a handy language for writing applications that link MySQL with the Web. Such an application can interface to the Web via the CGI.pm module and interface to MySQL using DBI.

+   * PHP is intended for design for writing Web applications, so that's obviously the environment to which it is best suited. For performance, database access is one of PHP's biggest strengths, so it's a natural choice for Web applications that perform MySQL-related tasks. It's possible to use PHP as a standalone interpreter (for example, to execute scripts from the shell), but it's not used that way very much.

Given these considerations, C and Perl are the most likely candidate languages if you're writing a standalone application. For Web applications, Perl and PHP are most suitable. If you need to write both types of applications, but don't know any of these languages and want to learn as few as possible, Perl might be your best option.

# ## 6.3.2 Performance

All other things being equal, we prefer to have applications run as quickly as possible. However, the actual importance of performance tends to be related to the frequency with which a program is used. For a program that you run once a month as a cron job during the night, performance might not matter that much. On the other hand, if you run a program many times a second on a heavily used Web site, even a bit of efficiency you gain can make a big difference. In the latter case, performance plays a significant role in the usefulness and appeal of your site. A slow site is annoying for visitors, no matter what the site is about, and if you depend on the site as a source of income, decreased performance translates directly into reduced revenue. You cannot service as many connections at a time, and visitors who tire of waiting give up and go elsewhere.

Performance assessment is a complex issue. The best indicator of how well your application will perform when written for a particular API is to write it under that API and try it. And the best comparative test is to implement multiple versions under different APIs to see how they stack up against each other. Of course, that's not how development usually works. More often, you just want to get your program written. After it's working, you can think about tuning it to see whether it can run faster or use less memory, or whether it has some other aspect that you can improve. But there are at least two general factors that you can count on as affecting performance in a relatively consistent way:

+   * Compiled programs execute more quickly than interpreted scripts.
+   * For interpreted languages used in a Web context, performance is better when the interpreter is invoked as a module that is part of the Web server itself rather than as a separate process.

# ### 6.3.2.1 Compiled Versus Interpreted Languages

As a general principle, compiled applications are more efficient, use less memory, and execute more quickly than an equivalent version of the program written in a scripting language. This is due to the overhead involved with the language interpreter that executes