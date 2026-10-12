```
```xml
<states>
  <lin-def:rpminfo_state id="oval:org.open-scap:cpe:rhel:ste:7" version="1">
    <lin-def:name operation="pattern match">^redhat-release</lin-def:name>
    <lin-def:version operation="pattern match">^7[\\d]</lin-def:version>
  </lin-def:rpminfo_state>
</states>
</oval_definitions>
```
```

# 7.2.3. The Data Stream Format

SCAP data stream is a file format used since SCAP version 1.2 and it represents a bundle of XCCDF, OVAL, and other component files which can be used to define a compliance policy expressed by an XCCDF checklist. It also contains an index and catalog that allow splitting the given data stream into files according to the SCAP components.

The data stream uses XML format that consists of a header formed by a table of contents and a list of the `<ds:component>` elements. Each of these elements encompasses an SCAP component such as XCCDF, OVAL, CPE, and other. The data stream file may contain multiple components of the same type, and thus covering all security policies needed by your organization.

# Example 7.3. An Example of a Data Stream Header

```
```xml
<ds:data-stream-collection
    xmlns:ds="http://scap.nist.gov/schema/scap/source/1.2"
    xmlns:xlink="http://www.w3.org/1999/xlink"
    xmlns:cat="urn:oasis:names:tc:entity:xmlns:xml:catalog"
    id="scap_org.open-scap_collection_from_xccdf_ssg-rhel7-xccdf-1.2.xml"
    schematron-version="1.0">
  <ds:data-stream id="scap_org.open-scap_datastream_from_xccdf_ssg-rhel7-xccdf-1.2.xml"
                 scap-version="1.2" use-case="OTHER">
    <ds:dictionaries>
      <ds:component-ref id="scap_org.open-scap_cref_output--ssg-rhel7-cpe-dictionary.xml"
                        xlink:href="#scap_org.open-scap_comp_output--ssg-rhel7-cpe-dictionary.xml">
        <cat:catalog>
          <cat:uri name="ssg-rhel7-cpe-oval.xml"
                   uri="#scap_org.open-scap_cref_output--ssg-rhel7-cpe-oval.xml"/>
        </cat:catalog>
      </ds:component-ref>
    </ds:dictionaries>
    <ds:checklists>
      <ds:component-ref id="scap_org.open-scap_cref_ssg-rhel7-xccdf-1.2.xml"
                        xlink:href="#scap_org.open-scap_comp_ssg-rhel7-xccdf-1.2.xml">
        <cat:catalog>
```
```