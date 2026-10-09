# CHAPTER FOURTEEN

# Using the Application Battery

The **LSB Application Battery** is a collection of several open source applications built to comply with the LSB Written Specification. The LSB project provides these applications to be used as further proof that a Linux distribution is able to support installation and execution of LSB-compliant applications.

Certification of a Linux distribution requires several methods to ensure compliance with the LSB Written Specification. The LSB Runtime test suite is used to test for the proper behavior of many of the system APIs. The LSB library checker verifies that all LSB-specified shared libraries and their respective APIs are present on the system. The third major test for compliance of a Linux distribution is the **LSB Application Battery**.

The choice of applications in the Battery is designed to exercise all of the LSB-specified shared libraries in a more real world situation. Using the Application Battery in this way complements the LSB Runtime test suite to provide a more thorough validation of a Linux distribution.

A further area where the **Application Battery** is useful is in its use of the **LSB Development Environment**. By using the Development Environment to build applications that use all of the LSB shared libraries, it helps to identify any deficiencies present in the header files and stub libraries of LSB Development Environment. Because the `lsbdev` is created directly from the data used in the Written Specification, it uncovers any problem with the specification itself.