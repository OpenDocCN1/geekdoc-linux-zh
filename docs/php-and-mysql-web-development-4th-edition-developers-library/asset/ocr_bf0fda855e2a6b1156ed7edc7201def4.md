# I.3.4 PDO Constants

This section describes some of the constants that can be used with PDO methods, such as the `getAttribute()` and `setAttribute()` methods for database handles. The values shown are representative only. For a complete list, see the PDO section of the PHP manual.

General database-handle attributes:

+   * `PDO::ATTR_AUTOCOMMIT`
+       The current autocommit mode.

+   * `PDO::ATTR_DEFAULT_FETCH_MODE`
+       The row-fetching mode. (Available as a database-handle attribute as of PHP 5.2.4.)

+   * `PDO::ATTR_DRIVER_NAME`
+       The PDO driver name.

+   * `PDO::ATTR_ERRMODE`
+       The error-handling mode. For a description of the allowable values, see Section I.3.3, “PDOException Object Methods” (online).

MySQL-specific database-handle attributes:

+   * `PDO::ATTR_CLIENT_VERSION`
+       A string describing the client library version.

+   * `PDO::ATTR_CONNECTION_STATUS`
+       For MySQL, this indicates how the connection was made.

+   * `PDO::ATTR_SERVER_INFO`
+       A string providing some server activity information.

+   * `PDO::ATTR_SERVER_VERSION`
+       A string describing the server version.

Fetch-mode values that control the form in which result set rows are fetched:

+   * `PDO::FETCH_ASSOC`
+       Return an array with elements accessed by associative index.

+   * `PDO::FETCH_BOTH`
+       Return an array with elements accessed by associative or numeric index.

+   * `PDO::FETCH_BOUND`
+       Return row elements bound to PHP variables by preceding `bindColumn()` calls.

+   * `PDO::FETCH_CLASS`
+       Return row elements into properties of a new class instance.

+   * `PDO::FETCH_INTO`
+       Return row elements into properties of an existing class instance.