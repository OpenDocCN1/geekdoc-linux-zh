```
| json
|   report.html
|   environment.json

1 directory, 5 files
```

The atomic scan generates a subdirectory with all the results and reports from a scan in the `/var/lib/atomic/openscap/` directory. The `arf.xml` file with results is generated on every scanning for configuration compliance. To generate a human-readable HTML report file, add the `report` suboption to the `--scanner_args` option.

To generate XCCDF results readable by DISA STIG Viewer, add the `stig-viewer` suboption to the `--scanner_args` option. The results are placed in `stig.xml`. For more information about DISA STIG Viewer, see Section 7.4.7, “Exporting XCCDF Results for the DISA STIG Viewer”

The `--scanner_args` suboptions are separated by the comma character. The specific values for the `xccdf-id` and `profile` suboptions, which select an XCCDF component and a profile from the specified datastream file, are taken from the bundled SCAP content in the OpenSCAP image. The datastream file is selected automatically by the OpenSCAP image during scanning based on the target container image or container.

> **NOTE**
> 
> When the `xccdf-id` suboption of the `--scanner_args` option is omitted, the scanner searches for a profile in the first XCCDF component of the selected datastream file. For more details about datastream files, see Section 7.2.3, “The Data Stream Format” .

# Remediating Configuration Compliance of Docker-formatted Images and Containers Using atomic scan

To remediate docker-formatted container images to the specified policy, add the `--remediate` option to the `atomic scan` command when scanning for configuration compliance. The following command builds a new remediated container image compliant with the DISA STIG policy from the Red Hat Enterprise Linux 7 container image:

```
atomic scan --remediate --scan_type configuration_compliance --scanner_args profile=xccdf_org.ssgproject.content_profile_stig-rhel7-disa,report
registry.access.redhat.com/rhel7:latest

The following issues were found:

Configure Time Service Maxpoll Interval
    Severity: Low
    XCCDF result: fail

Configure LDAP Client to Use TLS For All Transactions
    Severity: Moderate
    XCCDF result: fail

Remediating rule 43/44:
    'xccdf_org.ssgproject.content_rule_chronyd_or_ntpd_set_maxpoll'
Remediating rule 44/44:
    'xccdf_org.ssgproject.content_rule_ldap_client_start_tls'
```