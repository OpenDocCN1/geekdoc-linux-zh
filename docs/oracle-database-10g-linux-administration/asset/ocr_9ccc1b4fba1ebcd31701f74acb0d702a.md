the Oracle E-Business Suite is available on eight different platforms, also including Linux. It is not necessary that the application tier and the database tier reside on the same operating system. It is also acceptable for the application tier to be on a 32-bit system and the database tier to be on a 64-bit system. Both of these could be Linux systems, or a mix of Linux for the application tier and another operating system for the database tier, or vice versa.

I have personally been involved in migrations of the E-Business Suite from HP-UX and Solaris to Linux where the database tier is converted to Linux at a separate time from the application tier. Conversions can happen on different tiers at different times independently of the other tier.

Because of the complexity of the different modules and their interaction, the E-Business Suite installation includes all available modules. The ones that you use are based on the licensing acquired. Many of the different applications rely on each other. For example, Accounts Payable, Accounts Receivable, and other financials all rely on the General Ledger module.

# What Is the Oracle E-Business Suite?

The Oracle E-Business Suite is an integrated set of products designed to run your business, both front-office and back-office. The Oracle E-Business Suite is an extremely complex and huge application. The binaries themselves are in the tens of gigabytes in size. With Oracle E-Business Suite 11i, the entire suite is web-based and Forms-based and utilizes the Oracle Application Server 9i (OracleAS 9i) in order to run. However, since the installation is completely integrated, it is unnecessary to install the Oracle Application Server separately. The entire installation of all components is done through the Oracle E-Business Suite Rapid Installer, or rapidwiz.

The Oracle E-Business Suite is designed for fairly large businesses. The entire application is much too complex and requires too much maintenance for small businesses to utilize. It is necessary to have at least one full-time Oracle E-Business Suite DBA in order to properly maintain the E-Business Suite.

# E-Business Suite Architecture

The Oracle E-Business Suite is a multitiered application that can exist on one or more computer systems. There are multiple layers, or tiers, to the application, and depending on your needs, they can reside on the same, or multiple, systems. The various tiers consist of the following:

+   - Desktop tier This consists of the web browser used for the newer HTML-based applications, and an add-on Java applet to provide the traditional forms-based user interface.
+   - Application tier This layer, commonly referred to as the middle tier, is made up of a number of different components such as the Web Server,