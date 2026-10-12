```
system="urn:xccdf:fix:script:sh">
    yum -y remove
    <sub idref="xccdf_com.example.www_value_1"/>
    </fix>
    <check system="http://oval.mitre.org/XMLSchema/oval-definitions-5">"/>
    <check-export value-id="xccdf_com.example.www_value_1"
        export-name="oval:com.example.www:var:1"/>
    <check-content-ref href="example.oval.xml"
        name="oval:com.example.www:def:1"/>
    </check>
    <check system="http://open-scap.org/page/SCE">
        <check-import import-name="stdout"/>
        <check-content-ref href="telnetserver.sh"/>
    </check>
    </Rule>
    </Group>
</Benchmark>
```

# 7.2.2. The OVAL File Format

The Open Vulnerability Assessment Language (OVAL) is the essential and oldest component of SCAP. The main goal of the OVAL standard is to enable interoperability among security products. That is achieved by standardization of the following three domains:

+   1. Representation of the target system configuration.
+   2. Analysis of the target system for the presence of a particular machine state.
+   3. Reporting the results of the comparison between the specified machine state and the observed machine state.

Unlike other tools or custom scripts, the OVAL language describes a required state of resources in a declarative manner. The OVAL language code is never executed directly, but by means of an OVAL interpreter tool called scanner. The declarative nature of OVAL ensures that the state of the assessed system is not accidentally modified, which is important because security scanners are often run with the highest possible privileges.

OVAL specification is open for public comments and contribution and various IT companies collaborate with the MITRE Corporation, federally funded not-for-profit organization. The OVAL specification is continuously evolving and different editions are distinguished by a version number. The current version 5.11.1 was released in April 2015.

Like all other SCAP components, OVAL is based on XML. The OVAL standard defines several document formats. Each of them includes different kind of information and serves a different purpose.

# The OVAL Document Formats

+   - The OVAL Definitions format is the most common OVAL file format that is used directly for system scans. The OVAL Definitions document describes the required state of the target system.