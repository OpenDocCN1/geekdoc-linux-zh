220 Chapter 4 • Tuning the Shared Pool

# **FIGURE 4.10** *REPORT.TXT output showing Data Dictionary Cache statistics*

![](bbox=[0.26, 0.15, 0.85, 0.45])

Using this output and the formula 1–(Sum of the GET_MISS column + Sum of the GET_RSEQ column), you can calculate the Data Dictionary Cache hit ratio of this database to be 96.9 percent.

# # Improving Shared Pool Performance

Now that you know about the components of the Shared Pool and can measure the performance of each, you can examine methods for improving Shared Pool performance. The objective of all these methods is to increase Shared Pool performance by improving Library Cache and Data Dictionary Cache hit ratios. These techniques fall into five categories:

+   - Make it bigger
+   - Make room for large PL/SQL statements
+   - Keep important PL/SQL code in memory
+   - Encourage code reuse
+   - Tune Library Cache-specific init.ora parameters