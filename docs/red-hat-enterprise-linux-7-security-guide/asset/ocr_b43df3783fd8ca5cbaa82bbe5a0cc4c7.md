+   The OVAL Variables format defines variables used to amend the OVAL Definitions document. The OVAL Variables document is typically used in conjunction with the OVAL Definitions document to tailor the security content for the target system at runtime.
+   
+   The OVAL System Characteristics format holds information about the assessed system. The OVAL System Characteristics document is typically used to compare the actual state of the system against the expected state defined by an OVAL Definitions document.
+   
+   The OVAL Results is the most comprehensive OVAL format that is used to report results of the system evaluation. The OVAL Results document typically contains copy of the evaluated OVAL definitions, bound OVAL variables, OVAL system characteristics, and results of tests that are computed based on comparison of the system characteristics and the definitions.
+   
+   The OVAL Directives format is used to tailor verbosity of an OVAL Result document by either including or excluding certain details.
+   
+   The OVAL Common Model format contains definitions of constructs and enumerations used in several other OVAL schemes. It is used to reuse OVAL definitions in order to avoid duplications across multiple documents.

The OVAL Definitions document consists of a set of configuration requirements where each requirement is defined in the following five basic sections: definitions, tests, objects, states, and variables. The elements within the definitions section describe which of the tests shall be fulfilled to satisfy the given definition. The test elements link objects and states together. During the system evaluation, a test is considered passed when a resource of the assessed system that is denoted by the given object element corresponds with the given state element. The variables section defines external variables which may be used to adjust elements from the states section. Besides these sections, the OVAL Definitions document typically contains also the generator and signature sections. The generator section holds information about the document origin and various additional information related to its content.

Each element from the OVAL document basic sections is unambiguously identified by an identifier in the following form:

```
oval:namespace:type:ID
```

where namespace is a name space defining the identifier, type is either def for definitions elements, tst for tests elements, obj for objects element, ste for states elements, and var for variables elements, and ID is an integer value of the identifier.

# Example 7.2. An Example of an OVAL Definitions Document

```
<?xml version="1.0" encoding="utf-8"?>
<oval_definitions
    xmlns:lin-def="http://oval.mitre.org/XMLSchema/oval-definitions-5#linux"
    xmlns:oval="http://oval.mitre.org/XMLSchema/oval-common-5"
    xmlns="http://oval.mitre.org/XMLSchema/oval-definitions-5"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
<generator>
    <oval:product_name>vim</oval:product_name>
    <oval:schema_version>5.10.1</oval:schema_version>
    <oval:timestamp>2012-11-22T15:00:00+01:00</oval:timestamp>
</generator>
<definitions>
```