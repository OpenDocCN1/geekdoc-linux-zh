# **Example 7.11. Transforming an SSG XCCDF Scan Result into a Report**

To transform a result of an SSG XCCDF scan into an HTML file, enter the following command:

```
`~]$ oscap xccdf generate report scan-xccdf-results.xml > scan-xccdf-report.html`
```

The result report is stored as the ssg-scan-xccdf-report.html file in the current directory. Alternatively, you can generate this report in the time of the scan using the --report command-line argument:

```
`~]$ oscap xccdf eval --profile xccdf_org.ssgproject.content_profile_rht-ccp --results scan-xccdf-results.xml --report scan-xccdf-report.html /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml`
```

# **7.4.5. Validating SCAP Content**

Before you start using a security policy on your systems, you should first verify the policy in order to avoid any possible syntax or semantic errors in the policy. The oscap utility can be used to validate the security content against standard SCAP XML schemas. The validation results are printed to the standard error stream (stderr). The general syntax of such a validation command is the following:

```
`oscap module validate [module_options_and_arguments] file`
```

where file is the full path to the file being validated. The only exception is the data stream module (ds), which uses the sds-validate operation instead of validate. Note that all SCAP components within the given data stream are validated automatically and none of the components is specified separately, as can be seen in the following example:

```
`~]$ oscap ds sds-validate /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml`
```

With certain SCAP content, such as OVAL specification, you can also perform a Schematron validation. The Schematron validation is slower than the standard validation but provides deeper analysis, and is thus able to detect more errors. The following SSG example shows typical usage of the command:

```
`~]$ oscap oval validate --schematron /usr/share/xml/scap/ssg/content/ssg-rhel7-ds.xml`
```

# **7.4.6. Using OpenSCAP to Remediate the System**

OpenSCAP allows to automatically remediate systems that have been found in a non-compliant state. For system remediation, an XCCDF file with instructions is required. The scap-security-guide package contains certain remediation instructions.

System remediation consists of the following steps:

+   1. OpenSCAP performs a regular XCCDF evaluation.

+   2. An assessment of the results is performed by evaluating the OVAL definitions. Each rule that has failed is marked as a candidate for remediation.