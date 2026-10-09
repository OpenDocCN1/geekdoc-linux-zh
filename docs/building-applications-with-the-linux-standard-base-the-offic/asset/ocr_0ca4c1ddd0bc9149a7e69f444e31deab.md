# 7.2.5 Formal Testing for LSB Application Certification

Formal testing is a self-test activity whose results are submitted to the Certification Authority for audit, via the Web certification system. Only authorized test tools are valid for certification.

When a test campaign requires the warranty of the product working in a particular situation, or the warranty that selected applications execute correctly on the product, then a Web form will prompt for confirmation of that during the final registration stage and allow for a problem report ID to be referenced for any problems encountered.

# 7.2.5.1 Test Journals

Test results submitted should always include the full journal output from an uninterrupted run of the applicable test suite. If this is not possible, a problem report must be raised stating the nature of the problem and a response received from the Certification Authority before proceeding further.

Within the Web certification system, the supplier is required to upload test journals for each applicable test suite. The system also allows the supplier to obtain a summary report of the result status for a test journal. If this test journal is the formal certification test run for a product, the supplier must select the validation tool within the Web certification system. This will then automatically analyze the test results, and if there are no failed test results or tests requiring manual resolution, then the journal will be flagged as OK in the system. If there are failed test results detected by the validation tool, then a screen will be presented with a list of test cases that need to be resolved.

In the test journal, the failed test results that require resolution are those with a status of FAIL, UNINITIATED, UNRESOLVED, or UNREPORTED. The resolution process requires the supplier to enter a valid reference to an approved problem report from the Problem Reporting database for each failed test case. An approved problem report is one that has resulted in an agreed Interpretation of the specification, a Test Suite Deficiency, or a Certification System Deficiency. Each of these applies to a specific release of the specification, test suite, or certification system.