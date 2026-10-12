+   - Business intelligence
+   - E-business integration

# Java 2 Enterprise Edition

The Java 2 Enterprise Edition (J2EE) provides the industry standard for Java and is the means for developing multitier applications. The advantage for using J2EE is the “write once, run anywhere” paradigm. The benefit to this is obvious to anyone who manages application development and is responsible for its Return On Investment (ROI). J2EE is standardized and modular, allowing a robust service without the need for complicated programming efforts. J2EE generally includes services for Enterprise JavaBeans, JavaServer Pages, XML, and Java Servlets. The key benefit for using the J2EE platform is to quickly develop and deploy enterprise applications that are supported across several platforms and readily available over the Web.

J2EE applications can be rapidly deployed with OracleAS 10g, once an EAR file has been created. The EAR file can then be deployed into the J2EE container via a deployment wizard within the Enterprise Manager. This wizard maps all the relevant URLs to the correct web modules, sets up a persistence layer, and assigns a manager to the application.

Administration of J2EE applications is extended with the 10g Application Server, as OC4J containers can be added or configured, J2EE resources can be centralized, and applications can be monitored.

# Management and Security

This particular aspect of OracleAS 10g breaks down into several components that allow complete control and access to various applications within any desired scope. These components are

+   - **Oracle Enterprise Manager Application Server/Grid Control** The Oracle 10g Enterprise Manager allows for complete deployment and configuration of J2EE application servers. When coupled with Grid Control, the scope of monitoring and control is expanded to include other Oracle products and the host operating system.
+   - **Oracle Single Sign-On** With use of the available LDAP database, users can be authenticated from several applications with a single login ID. This makes Enterprise password maintenance much more manageable.
+   - **Oracle Application Server Certificate Authority** A centralized server for managing SSL support, this component includes key generation for client-side authentication to provide encrypted information transfer.