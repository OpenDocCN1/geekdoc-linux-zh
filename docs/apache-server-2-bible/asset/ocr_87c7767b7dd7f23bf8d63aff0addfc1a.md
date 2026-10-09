![](bbox=[0.74, 0.07, 0.93, 0.17])



# ## Installing and Running Apache for Windows

# ### In This Chapter

+   * System requirements for running Apache on Windows
+   * Installing Apache on Windows
+   * Starting, stopping, and restarting Apache

Although Apache has been ported to the Windows platform for a long time, **Apache 2.0** is the first version that can take advantage of native Windows system calls. All previous versions of Apache used a POSIX abstraction layer that degraded performance when Apache ran on Windows. Now Apache can finally compete head-to-head with other native Web servers such as Microsoft IIS and Netscape Enterprise server.

In this chapter, you learn about the system requirements for running Apache under popular Windows platforms such as Windows XP, Windows 2000, Windows NT, and Windows 9x/ME; you also learn to install Apache and to configure it so that you can get up and running fast.

# ## System Requirements

Apache requires that you have **TCP/IP** enabled on your Windows system. You should make sure that you have the latest **TCP/IP stack** (*Winsock*) for your Windows platform. Users of Windows 2000 with TCP/IP enabled can install Apache without any other Windows-specific requirements. Users of Windows NT 4.0 should ensure that the latest service packs are installed.

Windows 2000 Advanced Server is the ideal platform for running a production-grade Apache Web server. Windows 2000 Advanced Server is tuned for network services, so it should yield the best performance for Apache along with other Internet services.