![](bbox=[0.15, 0.11, 0.36, 0.28])

he previous chapter showed how to identify and remedy performance bottlenecks in an application's SQL code. This is a very important part of database tuning, as rewriting poorly performing SQL can make a huge difference in how well an Oracle-based application performs. However, rewriting application SQL in an effort to improve database performance is frequently not an option, particularly when production applications are involved or when third-party applications, whose SQL code you may not have access to, are being tuned. In these cases, you have options when it comes to tuning:

+   In the case of a purchased application, you can complain to the vendor and hope they do something about the poor performance.

+   You can add your own indexes to the delivered product in the hopes that they will improve performance.

+   You can tune Oracle's shared memory structure, the SGA (System Global Area), and try to improve application performance by minimizing the overhead associated with SQL statement processing and the accessing of the application's data and index blocks.

Realizing that the third option will probably result in the greatest performance gain, in the next four chapters we will address the issue of tuning the components of the Oracle SGA. This chapter deals with tuning the Shared Pool; Chapter 5, “Tuning the Database Buffer Cache,” discusses tuning the Database Buffer Cache, Chapter 6, “Tuning Other SGA Areas,” covers tuning the Large Pool, Java Pool, and Shared Server SGA components, and Chapter 7, “Tuning Redo Mechanisms,” discusses tuning the Redo Log Buffer.