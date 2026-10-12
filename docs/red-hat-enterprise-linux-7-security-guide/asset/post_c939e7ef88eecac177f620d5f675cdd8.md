
# 7.6.1. Scanning Docker-formatted Images and Containers for Vulnerabilities Using atomic scan

To scan the containers and container images, use the `atomic scan` command in the following form:

```
# atomic scan [OPTIONS] [ID]
```

where *ID* is the ID of the container image or container. To scan all container images or containers, use the `--images` or `--containers` directive, respectively. To scan both types, use the `--all` directive. The list of available command-line options can be obtained using the `atomic scan --help` command.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_229_0.png)

**NOTE**

For a detailed description of the `atomic` command usage and containers, see the Product Documentation for Red Hat Enterprise Linux Atomic Host. The Red Hat Customer Portal also provides a guide to the Atomic command line interface (CLI).

The default scan type of the `atomic scan` command is CVE scan. Use it for checking a target for known security vulnerabilities as defined in the CVE OVAL definitions released by Red Hat.

![](img/c62903c5bdbf5bcc6bc0ae8373bee5f4_229_1.png)

**WARNING**

The OVAL definitions used by the CVE scan type are bundled in the container image during the build process. Red Hat provides weekly updates of the container image. Always use the latest `OpenSCAP` container image to ensure the definitions are up to date. To find out version of the installed `OpenSCAP` container image:

```
# atomic help registry.access.redhat.com/rhel7/openscap | grep version
```

### Example 7.13. Scanning Red Hat Enterprise Linux 7 Container Images for Known Security Vulnerabilities

The following command scans the Red Hat Enterprise Linux 7 container image for known security vulnerabilities. The `--verbose` directive provides additional details.

```
# atomic scan --verbose registry.access.redhat.com/rhel7:latest
docker run -t --rm -v /etc/localtime:/etc/localtime -v /run/atomic/2017-11-01-14-55-37-758180:/scanin -v /var/lib/atomic/openscap/2017-11-01-14-55-37-758180:/scanout:rw,Z -v /etc/oscapd:/etc/oscapd:ro registry.access.redhat.com/rhel7/openscap oscapd-evaluate scan --no-standard-compliance --targets chroots-in-dir:///scanin --output /scanout WARNING: Can't import the 'docker' package. Container scanning functionality will be disabled.
INFO:Creating tasks directory at '/var/lib/oscapd/tasks' because it
didn't exist.
INFO:Creating results directory at '/var/lib/oscapd/results' because it
didn't exist.
INFO:Creating results work in progress directory at
'/var/lib/oscapd/work_in_progress' because it didn't exist.
INFO:Evaluated EvaluationSpec, exit_code=0.
INFO:Evaluated EvaluationSpec, exit_code=0.
INFO:[100.00%] Scanned target
'chroot:://scanin/db7a70a0414e589d7c8c162712b329d4fc670fa47dde721250fb9
fcdbed9cc2'

registry.access.redhat.com/rhel7:latest (db7a70a0414e589)

registry.access.redhat.com/rhel7:latest passed the scan

Files associated with this scan are in /var/lib/atomic/openscap/2017-11-01-14-55-37-758180.
```

The following command scans the Red Hat Enterprise Linux 7.2 container image with several known security vulnerabilities:

```
$ atomic scan registry.access.redhat.com/rhel7:7.2
docker run -t --rm -v /etc/localtime:/etc/localtime -v /run/atomic/2017-11-01-14-49-36-614281:/scanin -v /var/lib/atomic/openscap/2017-11-01-14-49-36-614281:/scanout:rw,Z -v /etc/oscapd:/etc/oscapd:ro
registry.access.redhat.com/rhel7/openscap openscap-evaluate scan --no-standard-compliance --targets chroots-in-dir://scanin --output /scanout

registry.access.redhat.com/rhel7:7.2 (98a88a8b722a718)
```

The following issues were found:

- **RHSA-2017:2832**: nss security update (Important)
    - Severity: Important
    - Rhsa URL: https://access.redhat.com/errata/RHSA-2017:2832
    - Rhsa ID: RHSA-2017:2832-01
    - Associated CVEs:
        - CVE ID: CVE-2017-7805
        - Cve URL: https://access.redhat.com/security/cve/CVE-2017-7805
- **RHSA-2017:2016**: curl security, bug fix, and enhancement update (Moderate)
    - Severity: Moderate
    - Rhsa URL: https://access.redhat.com/errata/RHSA-2017:2016
    - Rhsa ID: RHSA-2017:2016-01
    - Associated CVEs:
        - CVE ID: CVE-2016-7167
        - Cve URL: https://access.redhat.com/security/cve/CVE-2016-7167
- **RHSA-2017:1931**: bash security and bug fix update (Moderate)
    - Severity: Moderate
    - Rhsa URL: https://access.redhat.com/errata/RHSA-2017:1931
    - Rhsa ID: RHSA-2017:1931-01
    - Associated CVEs:
        - CVE ID: CVE-2016-0634
        - CVE URL: https://access.redhat.com/security/cve/CVE-2016-0634
        - CVE ID: CVE-2016-7543
        - CVE URL: https://access.redhat.com/security/cve/CVE-2016-7543
        - CVE ID: CVE-2016-9401
        - CVE URL: https://access.redhat.com/security/cve/CVE-2016-9401

Files associated with this scan are in `/var/lib/atomic/openscap/2017-11-01-14-49-36-614281`.

# 7.6.2. Scanning and Remediating Configuration Compliance of Docker-formatted Images and Containers Using `atomic scan`

Scanning for Configuration Compliance of Docker-formatted Images and Containers Using `atomic scan`

The `atomic scan` command also supports the `configuration_compliance` scan. Use this type of scanning to evaluate Red Hat Enterprise Linux-based container images and containers with the SCAP content provided by the SCAP Security Guide (SSG) bundled inside the **OpenSCAP** container image. This enables scanning against any profile provided by the SCAP Security Guide.

To list the SCAP content provided by the **OpenSCAP** image for the `configuration_compliance` scan, enter the following command:

```
# atomic help registry.access.redhat.com/rhel7/openscap
```

To verify compliance of the latest Red Hat Enterprise Linux 7 container image with the Defense Information Systems Agency Security Technical Implementation Guide (DISA STIG) policy and generate an HTML report from the scan:

```
# atomic scan --scan_type configuration_compliance --scanner_args xccdf-id=scap_org.open-scap_cref_ssg-rhel7-xccdf-1.2.xml,profile=xccdf_org.ssgproject.content_profile_stig-rhel7-disa,report registry.access.redhat.com/rhel7:latest
```

The output of the previous command contains the information about files associated with the scan at the end:

```
........................
Files associated with this scan are in /var/lib/atomic/openscap/2017-11-03-13-35-34-296606.
# tree /var/lib/atomic/openscap/2017-11-03-13-35-34-296606
/var/lib/atomic/openscap/2017-11-03-13-35-34-296606
└─ db7a70a0414e589d7c8c162712b329d4fc670fa47ddde721250fb9fcdbed9cc2
   └─ arf.xml
   └─ fix.sh
   └─ json
   └─ report.html
   └─ environment.json

1 directory, 5 files
```

The `atomic scan` generates a subdirectory with all the results and reports from a scan in the `/var/lib/atomic/openscap/` directory. The `arf.xml` file with results is generated on every scanning for configuration compliance. To generate a human-readable HTML report file, add the `report` suboption to the `--scanner_args` option.

To generate XCCDF results readable by DISA STIG Viewer, add the `stig-viewer` suboption to the `--scanner_args` option. The results are placed in `stig.xml`. For more information about DISA STIG Viewer, see Section 7.4.7, “Exporting XCCDF Results for the DISA STIG Viewer”.

The `--scanner_args` suboptions are separated by the comma character. The specific values for the `xccdf-id` and `profile` suboptions, which select an XCCDF component and a profile from the specified datastream file, are taken from the bundled SCAP content in the OpenSCAP image. The datastream file is selected automatically by the OpenSCAP image during scanning based on the target container image or container.

> **NOTE**
>
> When the `xccdf-id` suboption of the `--scanner_args` option is omitted, the scanner searches for a profile in the first XCCDF component of the selected datastream file. For more details about datastream files, see Section 7.2.3, “The Data Stream Format”.

### Remediating Configuration Compliance of Docker-formatted Images and Containers Using atomic scan

To remediate docker-formatted container images to the specified policy, add the `--remediate` option to the `atomic scan` command when scanning for configuration compliance. The following command builds a new remediated container image compliant with the DISA STIG policy from the Red Hat Enterprise Linux 7 container image:

```
atomic scan --remediate --scan_type configuration_compliance --scanner_args profile=xccdf_org.ssgproject.content_profile_stig-rhel7-disa,report registry.access.redhat.com/rhel7:latest

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
