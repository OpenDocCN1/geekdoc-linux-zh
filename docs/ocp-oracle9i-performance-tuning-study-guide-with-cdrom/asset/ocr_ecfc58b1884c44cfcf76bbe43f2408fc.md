# TopSessions

TopSessions is a graphical tool for identifying in real time which users are consuming the most server resources. Resources that can be monitored include CPU, memory, file I/O, and transaction volume. Figure 2.9 shows a sample TopSessions screen.

# FIGURE 2.9 TopSessions Screen

![](bbox=[0.27, 0.26, 0.92, 0.65])

TopSessions is also useful for identifying locking issues, which may cause excessive waits for other database users. Locking is discussed in detail in Chapter 9, "Tuning Contention."

# Trace Data Viewer

Many Oracle servers are accessed by applications that are not Oracle-centric in nature. These applications only use the Oracle database as a repository for the application's data. All the application logic and processing happens outside the database. Gathering and analyzing performance data from these types of applications can be difficult. Oracle's Trace Data Viewer GUI tool allows you to collect performance data for specific events within these types of applications. This is accomplished through the use of an Application