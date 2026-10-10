
These security feature requirements may have to be interpreted when applying the criteria to specific systems with their own functional requirements, applications, or special environments (e.g., communications processors, process control computers, and embedded systems in general). The underlying assurance requirements can be applied across the entire spectrum of ADP system or application processing environments without special interpretation.

For this class of systems, the test conditions should be generated from the system documentation, which includes the Security Features User's Guide (SFUG), the Trusted Facility Manual (TFM), the system reference manual describing each Trusted Computing Base (TCB) primitive, and the design documentation defining the protection philosophy and its TCB implementation. Both the SFUG and the manual pages illustrate, for example, how the identification and authentication mechanisms work and whether a particular TCB primitive contains relevant security and accountability mechanisms. The Discretionary Access Control (DAC) and the identification and authentication conditions enforced by each primitive (if any) are used to define the test conditions of the test plans.

## Test Coverage

Testing shall be done to assure that there are no obvious ways for an unauthorized user to bypass or otherwise defeat the security protection mechanisms of the TCB [TCSEC, Part I, Section 2.1].

The team shall independently design and implement at least five system-specific tests in an attempt to circumvent the security mechanisms of the system [TCSEC, Part II, Section 10].

These two TCSEC requirements/guidelines define the scope of security testing for this security class. Since each TCB primitive may include security-relevant mechanisms, security testing will include at least five test conditions for each primitive. Furthermore, because source code analysis is neither required nor suggested for class C1 systems, monolithic functional testing (i.e., a black-box approach) with boundary-value coverage represents an adequate testing approach for this class. Boundary-value coverage of each test condition requires that at least two calls of each TCB primitive be made, one for the positive and one for the negative outcome of the condition. Such coverage may also require more than two calls per condition.

Whenever a TCB primitive refers to multiple types of objects, each condition is repeated for each relevant type of object for both its positive and negative outcomes. A large number of test calls may be necessary for each TCB primitive because each test condition may in fact have multiple related conditions, which should be tested independently of each other.

## Security Class C2: Test Condition Generation

Testing shall also include a search for obvious flaws that would allow violation of resource isolation, or that would permit unauthorized access to the audit and authentication data [TCSEC, Part I, Section 2.2].

These added requirements refer only to new sources of test conditions, not to a new testing approach, nor to new coverage methods. The following new sources of test conditions should be considered:

- **Resource isolation conditions.** These test conditions refer to all TCB primitives that implement specific system resources (e.g., object types or system services). Test conditions for TCB primitives implementing services may differ from those for TCB primitives implementing different types of objects. Thus, new conditions may need to be generated for TCB services. The mere repetition of test conditions defined for other TCB primitives may not be adequate for some services.
- **Conditions for protection of audit and authentication data.** Because both audit and authentication mechanisms and data are protected by the TCB, the test conditions for the protection of these mechanisms and their data are similar to those that show that the TCB protection mechanisms are tamperproof and noncircumventable. For example, these conditions show that neither privileged TCB primitives nor audit and user authentication files are accessible to regular users.

## Test Coverage

Although class C1 test coverage suggests that each test condition be implemented for each type of object, coverage of resource-specific test conditions also requires that each test condition be included for each type of service (whenever the test condition is relevant to a service). For example, the test conditions that show that direct access to a shared printer is denied to a user will be repeated for a shared tape drive with appropriate modification of test data (i.e., test environments setup, test parameters, and outcomes).

## Security Class B1: Test Condition Generation

The objectives of security testing shall be: to uncover all design and implementation flaws that would permit a subject external to the TCB to read, change, or delete data normally denied under the mandatory or discretionary security policy enforced by the TCB; as well as to ensure that no subject (without authorization to do so) is able to cause the TCB to enter a state such that it is unable to respond to communications initiated by other users [TCSEC, Part I, Section 3.1].

The security-testing requirements of class B1 are more extensive than those of either class C1 or C2, both in test condition generation and in coverage analysis. The source of test conditions referring to users' access to data includes the mandatory and discretionary policies implemented by the TCB. These policies are defined by an informal policy model whose interpretation within the TCB allows the derivation of test conditions for each TCB primitive. Although not explicitly stated in the TCSEC, it is generally expected that all relevant test conditions for classes C1 and C2 also would be used for a class B1 system.

## Test Coverage

All discovered flaws shall be removed or neutralized and the TCB retested to demonstrate that they have been eliminated and that new flaws have not been introduced [TCSEC, Part I, Section 3.1].

The team shall independently design and implement at least fifteen system specific tests in an attempt to circumvent the security mechanisms of the system [TCSEC, Part II, Section 10].

Although the coverage analysis is still boundary-value, security testing for class B1 systems suggests that at least 15 test conditions be generated for each TCB primitive that contains security-relevant mechanisms, to cover both mandatory and discretionary policies. In practice, however, a substantially higher number of test conditions is generated from interpretations of the (informal) security model. The removal or the neutralization of found errors, and the retesting of the TCB, requires no additional types of coverage analysis.

## Security Class B2: Test Condition Generation

Testing shall demonstrate that the TCB implementation is consistent with the descriptive top-level specification [TCSEC, Part I, Section 3.2].

This requirement implies that both the test conditions and coverage analysis of class B2 systems are more extensive than those of class B1. In class B2 systems, every access control and accountability mechanism documented in the descriptive top-level specification (DTLS) (which must be complete as well as accurate) represents a source of test conditions. In principle, the same types of test conditions would be generated for class B2 systems as for class B1 systems, because, first, in both classes, the test conditions could be generated from interpretations of the security policy model (informal at B1 and formal at B2), and, second, in class B2, the DTLS includes precisely the interpretation of the security policy model. In practice, however, this is not the case because security policy models do not model a substantial number of mechanisms that are, nevertheless, included in the DTLS of class B2 systems. The number and type of test conditions can therefore be substantially higher in a class B2 system than in a class B1 system, because the DTLS for each TCB primitive may contain additional types of mechanisms, such as those for trusted facility management.

## Test Coverage

It is not unusual to have a few individual test conditions for at least some of the TCB primitives. As suggested in the approach defined in the previous section, repeating these conditions for many of the TCB primitives to achieve uniform coverage can be both impractical and unnecessary. This is particularly true when these primitives refer to the same object types and services. For this reason, and because source-code analysis is required in class B2 systems to satisfy other requirements, the use of the gray-box testing approach is recommended for those parts of the TCB in which primitives share a substantial portion of their code. Note that the DTLS of any system does not necessarily provide any test conditions for demonstrating the tamper-proof capability and noncircumventability of the TCB. Such conditions should be generated separately.

## Kickoff

The cyber-criminal definitions, profiles, and security class information guidelines are provided to give an indication of the extent and sophistication of the highly recommended hack attack penetration testing, covered in the rest of this book. Individuals and organizations wishing to use the “Department of Defense Trusted Computer System Evaluation Criteria,” along with underground hacker techniques for performing their own evaluations, may find the following chapters useful for purposes of planning and implementation.
