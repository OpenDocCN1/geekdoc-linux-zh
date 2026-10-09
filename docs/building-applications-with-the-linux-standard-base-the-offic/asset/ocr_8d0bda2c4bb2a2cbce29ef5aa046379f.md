+   - Is the application installed into /opt/package/ or /opt/provider/ ?
+   - Is the application to be invoked by the end user via the library installed into /opt/package/bin/ or /opt/provider/bin/ ?
+   - Are the man pages of the application installed in /opt/package/man/ or /opt/provider/man/ ?
+   - Are the variable files of the application created in /var/opt/package/ or /var/opt/provider/ ?
+   - Are the host-specific configuration files of the application kept in /etc/opt/ ?
+   - Are there other package files that reside outside /opt/, /var/opt/, and /etc/opt/ (e.g., /var/lock/ or /var/run/)?

# 7.2.2.2  Authorized Test Suites

It should be noted that, for formal testing for LSB Application certification, only currently authorized versions of the LSB certification test suites can be used. So, for informal testing it is vital that an authorized version is also used to avoid later problems. The Certification Authority maintains a list of the currently authorized certification test suites.$ ^{2} $Since the test suites come from multiple sources, this online document includes information on how to obtain the test suites.

# 7.2.3  Registering an LSB Application Product within the Web Certification System

The LSB Application certification uses the same Web certification system as for the LSB Runtime Environment certification. For brevity, we include an overview in this chapter detailing the differences of LSB Application certification. See also Chapter 6 for more details on a Conformance Statement, product amendments, and renewals that apply equally to LSB Application certification.