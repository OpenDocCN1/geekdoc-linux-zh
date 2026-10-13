
## Table 25-3 Continued

| Parameter | Description |
|---|---|
| `--without-gd` | Build PHP without support for the GD graphics library. |
| `--with-gd=<directory>` | Indicates that PHP should be built with support for the GD graphics library and optionally specifies the path to the GD installation directory. |
| `--with-ttf=<directory>` | Indicates that PHP should be built with support for the FreeType font library and optionally specifies the path to the FreeType files. |
| `--enable-freetype-4bit-antialias-hack` | Build PHP with patches needed to support the FreeType 2 font library. |
| `--enable-t1lib` | Build GD support for PHP with t1lib support. |
| `--with-gettext=<directory>` | Indicates that PHP should be built with support for GNU gettext and optionally specifies the path to the GNU gettext files. If no path is specified, the default is `/usr/local`. |
| `--with-imagick=<directory>` | Indicates that PHP should be built with support for ImageMagick and optionally specifies the path to ImageMagick. If no path is specified, PHP will attempt to determine the location. |
| `--with-x` | Build PHP with support for X Windows. |
| `--with-oracle=<directory>` | Indicates that PHP should be built with support for Oracle databases and optionally specifies the path to the Oracle home directory. If no path is specified, the default is the value of the `ORACLE_HOME` environment variable. |
| `--with-iodbc=<directory>` | Indicates that PHP should be built with support for the iODBC ODBC driver package and optionally specifies the location of the iODBC base installation directory. If no path is specified, the default value is `/usr/local`. |
| `--with-openlink=<directory>` | Indicates that PHP should be built with support for the OpenLink ODBC driver package and optionally specifies the location of the OpenLink base installation directory. If no path is specified, the default value is `/usr/local/openlink`. |
| `--with-adabas=<directory>` | Indicates that PHP should be built with support for the Adabas D database and optionally specifies the location of the Adabas D base installation directory. If no path is specified, the default value is `/usr/local`. |
| `--with-sybase=<directory>` | Indicates that PHP should be built with support for the Sybase database and optionally specifies the location of the Sybase home directory. If no path is specified, the default value is `/home/sybase`. |
| `--with-sybase-ct=<directory>` | Indicates that PHP should be built with support for Sybase-CT and optionally specifies the location of the Sybase home directory. If no path is specified, the default value is `/home/sybase`. |
| `--with-mysql=<directory>` | Indicates that PHP should be built with support for the MySQL database and optionally specifies the location of the MySQL installation directory. If no path is specified, PHP attempts to determine the location of the installation directory. |
| `--with-msql=<directory>` | Indicates that PHP should be built with support for the mSQL database and optionally specifies the location of the mSQL installation directory. If no path is specified, the default value is `/usr/local/Hughes`. |
| `--with-pgsql=<directory>` | Indicates that PHP should be built with support for the PostgreSQL database and optionally specifies the location of the PostgreSQL base installation directory. If no path is specified, the default value is `/usr/local/pgsql`. |
| `--with-ibm-db2=<directory>` | Indicates that PHP should be built with support for the IBM DB2 database and optionally specifies the location of the DB2 base installation directory. If no path is specified, the default value is `/home/db2inst1/sqllib`. |
| `--with-solid=<directory>` | Indicates that PHP should be built with support for the Solid database and optionally specifies the location of the Solid base installation directory. If no path is specified, the default value is `/usr/local/solid`. |
| `--with-empress=<directory>` | Indicates that PHP should be built with support for the Empress database and optionally specifies the location of the Empress base installation directory. If no path is specified, the default value is the value of the `EMPRESSPATH` environment variable. |
| `--with-ldap=<directory>` | Indicates that PHP should be built with support for LDAP and optionally specifies the location of the LDAP base installation directory. If no path is specified, the default value is `/usr` and `/usr/local`. |
| `--with-mck=<directory>` | Indicates that PHP should be built with support for Cybercash MCK and optionally specifies the location of the Cybercash MCK build directory. If no path is specified, the default value is `/usr/src/mck-3.2.0.3-linux`. |
| `--with-snmp=<directory>` | Indicates that PHP should be built with support for SNMP and optionally specifies the location of the SNMP base installation directory. If no path is specified, PHP attempts to locate the SNMP installation directory. |
| `--with-velocis=<directory>` | Indicates that PHP should be built with support for Velocis and optionally specifies the location of the Velocis base installation directory. If no path is specified, the default value is `/usr/local/velocis`. |
| `--with-informix=<directory>` | Indicates that PHP should be built with support for the Informix database and optionally specifies the location of the Informix base installation directory. |
| `--with-interbase=<directory>` | Indicates that PHP should be built with support for the Interbase database and optionally specifies the location of the Interbase base installation directory. If no path is specified, the default value is `/usr/interbase`. |
| `--with-custom-odbc=<directory>` | Indicates that PHP should be built with support for user-defined ODBC drivers and optionally specifies the location of the ODBC drivers. If no path is specified, the default value is `/usr/local`. |
| `--with-hyperwave` | Build PHP with Hyperwave support. |
| `--with-xml` | Build PHP with XML support. |
| `--with-yp` | Build PHP with support for YP (NIS). |
| `--with-zlib=<directory>` | Indicates that PHP should be built with support for zlib and optionally specifies the location of the zlib installation directory. If no path is specified, the default value is `/usr`. |
| `--with-pdflib=<directory>` | Indicates that PHP should be built with support for pdflib and optionally specifies the location of the pdflib installation directory. If no path is specified, the default value is `/usr/local`. |
| `--with-zlib-dir=<directory>` | Indicates the zlib directory for pdflib 2.0 or indicates that zlib support should be included if pdflib is not being included. |
| `--with-jpeg-dir=<directory>` | Indicates the JPEG directory for pdflib 2.0. |
| `--with-tiff-dir=<directory>` | Indicates the TIFF directory for pdflib 2.0. |
| `--with-cpdflib=<directory>` | Indicates that PHP should be built with support for ClibPDF and optionally specifies the location of the CLibPDF installation directory. If no path is specified, the default value is `/usr/local`. |
| `--with-fdftk=<directory>` | Indicates that PHP should be built with support for fdftk and optionally specifies the location of the fdftk installation directory. If no path is specified, the default value is `/usr/local`. |
| `--with-dbase` | Indicates that PHP should be built with the bundled support for Dbase databases. |
| `--with-filepro` | Indicates that PHP should be built with the bundled read-only support for FilePro databases. |
| `--with-mod-dav=<directory>` | Indicates that Apache should be built with DAV support through Apache’s `mod_dav` module and indicates the location of the `mod_dav` installation directory. |
| `--disable-unified-odbc` | Indicates that unified ODBC support should be disabled if iODBC, Adabas, Solid, Velocis or custom ODBC is enabled. |
| `--with-config-file-path=<directory>` | Specifies the path where PHP should look for the `php3.ini` file. By default, PHP will look in `/usr/local/lib`. |
| `--enable-debug` | Build PHP with debugging symbols enabled. |
| `--enable-safe-mode` | Build PHP with safe mode enabled by default. |
| `--with-exec-dir=<directory>` | Indicates that PHP should only allow executable scripts in the specified directory when running in safe mode. By default, PHP only allows executables in `/usr/local/php/bin` when running in safe mode. |
| `--enable-track-vars` | Indicates that support for GET, POST and Cookies tracking variables should be enabled by default. |
| `--enable-magic-quotes` | Indicates that magic quotes should be enabled by default. |
| `--enable-debugger` | Build PHP with support for remote debugging. |
| `--disable-bcmath` | Build PHP without bc-style precision math support. |
| `--enable-force-cgi-redirect` | Indicates that the security check for the internal server should be enabled. |
| `--enable-discard-path` | Allows the PHP CGI binary to be placed outside the Web document tree for security reasons when using PHP through CGI. |
| `--enable-memory-limit` | Build PHP with memory limit support. |
| `--disable-short-tags` | Disable support for the short-form `<?` Start tag by default. |
| `--disable-url-fopen-wrapper` | Disable the URL-aware fopen wrapper which allows PHP to access files through HTTP or FTP. |
| `--enable-sysvsem` | Build PHP with System V semaphore support. |
| `--enable-sysvshm` | Build PHP with System V shared memory support. |
| `--disable-display-source` | Build PHP without support for displaying source code. |
