TCB services. The mere repetition of test conditions defined for other TCB primitives may not be adequate for some services.

+   - *Conditions for protection of audit and authentication data.* Because both audit and authentication mechanisms and data are protected by the TCB, the test conditions for the protection of these mechanisms and their data are similar to those that show that the TCB protection mechanisms are tamperproof and noncircumventable. For example, these conditions show that neither privileged TCB primitives nor audit and user authentication files are accessible to regular users.

# Test Coverage

Although class C1 test coverage suggests that each test condition be implemented for each type of object, coverage of resource-specific test conditions also requires that each test condition be included for each type of service (whenever the test condition is relevant to a service). For example, the test conditions that show that direct access to a shared printer is denied to a user will be repeated for a shared tape drive with appropriate modification of test data (i.e., test environments setup, test parameters, and outcomes).

# *Security Class B1: Test Condition Generation*

The objectives of security testing shall be: to uncover all design and implementation flaws that would permit a subject external to the TCB to read, change, or delete data normally denied under the mandatory or discretionary security policy enforced by the TCB; as well as to ensure that no subject (without authorization to do so) is able to cause the TCB to enter a state such that it is unable to respond to communications initiated by other users *\[TCSEC, Part I, Section 3.1].*

The security-testing requirements of class B1 are more extensive than those of either class C1 or C2, both in test condition generation and in coverage analysis. The source of test conditions referring to users' access to data includes the mandatory and discretionary policies implemented by the TCB. These policies are defined by an informal policy model whose interpretation within the TCB allows the derivation of test conditions for each TCB primitive. Although not explicitly stated in the TCSEC, it is generally expected that all relevant test conditions for classes C1 and C2 also would be used for a class B1 system.

# Test Coverage

All discovered flaws shall be removed or neutralized and the TCB retested to demonstrate that they have been eliminated and that new flaws have not been introduced *\[TCSEC, Part I, Section 3.1].*

The team shall independently design and implement at least fifteen system specific tests in an attempt to circumvent the security mechanisms of the system *\[TCSEC, Part II, Section 10].*

Although the coverage analysis is still boundary-value, security testing for class B1 systems suggests that at least 15 test conditions be generated for each TCB primitive that contains security-relevant mechanisms, to cover both mandatory and discretionary policies. In practice, however, a substantially higher number of test conditions is generated from interpretations of the (informal) security model. The removal or the neutralization of found errors, and the retesting of the TCB, requires no additional types of coverage analysis.

# *Security Class B2: Test Condition Generation*

Testing shall demonstrate that the TCB implementation is consistent with the descriptive top-level specification *\[TCSEC, Part I, Section 3.2].*