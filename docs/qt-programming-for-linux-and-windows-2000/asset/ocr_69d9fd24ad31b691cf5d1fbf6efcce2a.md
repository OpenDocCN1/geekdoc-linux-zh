# Configuration Management

Within production environments, a conscientious IT management staff can institute comprehensive configuration management (CM) policies that prevent the installation of shared material until it has passed an approved battery of compatibility testing. This will prove sufficient in most cases, but introduces severe limitations on the installation of new or updated software since all changes have to be approved by the IT department. That usually takes a very long time.

Development environments should match the end-user environment as closely as possible to avoid costly delays that result from oversights in shared resource version control. This implies the same restrictions on installation of new software and updates as the production environment, although a development team usually has more flexibility in this regard.

The testing and quality-control environments should be maintained by the IT staff, with all the restrictions of the production environment. There may be additional restrictions imposed by the IT staff, relating to network access, access to critical production data repositories, and other critical resources.

# Total Static Linkage

Total static linkage is achieved by linking only to the static versions of all the libraries an application uses. While complete static linkage of an application is usually frowned on by developers and IT professionals alike, there are some clear advantages that should be weighed against the rescue costs:

+   - A statically linked application will never experience a shared library version mismatch failure or a library incompatibility issue. Ever.
+   - A completely static linkage application can be run on any binary-compatible system without installing additional support libraries, so dependency tracking is a simple task, and little regard need be given to target environment.
+   - When your application is the only application that will use its library's routines, and only one instance of that application is likely to execute at a time, a statically linked version will use fewer system resources than a dynamically linked version, and startup time will be significantly reduced. Remember, there is system overhead involved in shared library management.

# Mixed Static/Dynamic Linkage

This is a fairly common tradeoff, used by many vendors to reduce the risk of compatibility issues, while providing some of the benefits associated with dynamic linkage. It involves statically linking the application with any libraries aren't *guaranteed* to be present on the target platform, and dynamically linking with libraries that can safely be assumed to exist on the target platform. The Netscape product family uses this approach with a large degree of success. Communicator was traditionally provided in two varieties for many flavors of UNIX systems: dynamic or static Motif linkage. The base C library was dynamically linked in either.