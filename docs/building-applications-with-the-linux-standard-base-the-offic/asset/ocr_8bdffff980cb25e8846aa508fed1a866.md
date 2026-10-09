# CHAPTER ELEVEN

# Using the LSB Test Suites

This chapter describes the LSB Test Suites, how to obtain them, how to use them, and how to add more conformance tests.

# 11.1 UNDERSTANDING THE LSB TEST SUITES

The LSB Test Suites are a family of test suites for testing various aspects of the LSB. They include tests supplied in RPM format for testing LSB Runtime Environments for conformance to the LSB Written Specification. The tests are built in the LSB Development Environment to ensure they are LSB-conformant.

The test suites include both TET-based and non-TET-based tests. The Test Environment Toolkit (TET) is a framework and application program interface for test generation. The following sections describes each test.

# 11.1.1 TET-Based Tests

# 11.1.1.1 lsb-runtime-test

This test program is made up of a number of separate test modules combined into a single binary RPM.

POSIX.1-1990 test suite Runtime tests for compliance against the POSIX.1-1990 standard.