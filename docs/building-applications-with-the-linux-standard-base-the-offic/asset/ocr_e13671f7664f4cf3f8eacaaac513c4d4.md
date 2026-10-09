# ### 11.4.2 Writing TET-Based Test Suites

This section will help you understand the test development process at a high level. This process includes the following high level steps.

# #### 11.4.2.1 Developing the Specification

The specification should include the following information about the test suite:

+   * Test methodology
+   * Functional coverage
+   * Test architecture
+   * Assumptions
+   * Development schedule

# #### 11.4.2.2 Developing the Set of Formal Assertions

The purpose of this step is to create a list of testable statements from the specification. This is an intermediate step between the language of the specification and actual test code.

Formal test assertions should bridge the gap between the language of the specification and the test suite code. Likewise, the goal of the test code is to produce an executable representation of the requirements of the specification. Test suites developed with the assertion-based technique should meet the following requirements:

+   * They must follow the IEEE Standard for test methods (1003.3).
+   * An assertion must be developed for each definitive statement in the specification under the test.
+   * Each assertion must be designed to test whether the statement is true or false for the implementation under test.