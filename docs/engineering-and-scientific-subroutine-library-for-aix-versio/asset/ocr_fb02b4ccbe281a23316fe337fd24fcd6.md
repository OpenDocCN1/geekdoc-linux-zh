Table 33. Product File Set Names for ESSLL for AIX (continued)
| Product File Sets | Descriptive Name |
|---|---|
| vac.C | C for AIX Compiler |
| vacpp.cmp.C | VisualAge C++ Professional for AIX Compiler |

**On Linux** Enter the following command: `rpm -q *package*`
where the appropriate values of *package* are listed in Table 34.

Table 34. Package Names for ESSLL for Linux
| Product Package | Descriptive Name |
|---|---|
| essl.rte | ESSLL |
| xlf.rte | XL Fortran Run-Time Environment |
| xlsmp.rte | SMP Run-Time Environment |
| xlf.cmp | XL Fortran Compiler |
| vac.cmp | C for Linux Compiler |
| vacpp.cmp | VisualAge C++ Professional for Linux Compiler |

+   5. The message that is returned when an error is detected.
+   6. Any error message relating to core dumps.
+   7. The compiler listings, including compiler options in effect, and any run-time listings produced
+   8. Program changes made in comparison with a previous successful run
+   9. A small test case demonstrating the problem using the minimum number of statements and variables, including input data
+   Consult your IBM Service representative for more assistance.

# National Language Support

For National Language Support (NLS), all ESSLL subroutines display messages located in externalized message catalogs. English versions of the message catalogs are shipped with the product, but your site may be using its own translated message catalogs. The environment variable **NLSPATH** is used by the various ESSLL subroutines to find the appropriate message catalog. **NLSPATH** specifies a list of directories to search for message catalogs. The directories are searched, in the order listed, to locate the message catalog. In resolving the path to the message catalog, **NLSPATH** is affected by the value of the environment variables **LC_MESSAGES** and **LANG**.

The ESSLL message catalogs are in English, and are located in the following directories:

+   **On AIX** `/usr/lib/nls/msg/C`
+   `/usr/lib/nls/msg/En_US`
+   `/usr/lib/nls/msg/en_US`
+   **On Linux** `/usr/share/locale/en_US/LC_MESSAGES`
+   `/usr/share/locale/C`