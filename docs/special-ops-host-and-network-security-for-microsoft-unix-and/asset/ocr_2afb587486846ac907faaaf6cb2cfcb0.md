# Table 13.2 Summary of Vulnerabilities

| Vulnerability | Description |
| :--- | :--- |
| Format string vuln in PL/SQL module | A format string vuln has been discovered in the PL/SQL module of 9iAS that allows modification of heap-based memory. |
| PL/SQL injection in genpopuplist | Arbitrary SQL commands can be injected into the *p* parameter of the PORTAL.genpopuplist function. |
| PL/SQL injection in PORTAL_www_ui_lof | Arbitrary SQL commands can be injected using the PORTAL_www_ui_lof function. |
| PL/SQL injection in PORTAL_wwa_app_module | Arbitrary SQL commands can be injected into the *p* parameter of the PORTAL_wwa_app_module function. |
| PL/SQL injection in PORTAL_www_dynxml_generator | Arbitrary SQL commands can be injected into the *p* parameter of the PORTAL_www_dynxml_generator function. |
| PL/SQL injection in PORTAL_DEMO_ORG_CHART | Arbitrary SQL commands can be injected into the *p* parameter of the PORTAL_DEMO_ORG_CHART function. |
| Buffer overflow in PL/SQL module | A buffer overflow exists in the PL/SQL module of Oracle Application Server. The overflow occurs when a request is made to the admin section of a PL/SQL SAD with a long string. |
| PL/SQL administrative access | By default, any user can access the PL/SQL administrative pages and modify the existing DAOs. |
| PL/SQL authorization denial of service | When a malformed field is sent to the Web server in the Authorization field of the HTTP header, the Apache server will crash. |
| PL/SQL directory traversal | A double decoding problem exists in the PL/SQL module that allows an attacker to break out of the Web site directories. |

owa_util.showsource code disclosure

The function *owa_util.showsource* can be used by Web users to view the source of your application.

owa_util.cellsprint arbitrary query execution

The function *owa_util.cellsprint* can be used by Web users to execute arbitrary select statements.