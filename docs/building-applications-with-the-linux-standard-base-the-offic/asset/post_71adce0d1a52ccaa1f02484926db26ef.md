
## 10.2 PRODUCT STANDARD DESCRIPTIONS

*A product standard* is a concise statement identifying those parts of the LSB Written Specification that must be implemented in a product carrying the LSB brand.

**LSB Runtime Environment** *The LSB Runtime Environment for IA32* (or other architectures) product standard is for platforms providing services that conform to the LSB specifications, specifically the LSB 2.0 common specification (known as gLSB or LSB-Core), in conjunction with the LSB specification for the IA32 (or other architectures) Architecture 2.0 processor-specific supplement (known as archLSB or LSB-Core-IA32). For more details, see Section 6.3.4.1.

**LSB Application** *The LSB Application for IA32* (or other architectures) product standard is for applications conforming to the LSB specifications, specifically the LSB 2.0 common specification (known as gLSB or LSB-Core), in conjunction with the LSB specification for the IA32 (or other architectures) Architecture 2.0 processor-specific specification (known as archLSB or LSB-Core-IA32). LSB Applications are the consumers of services provided by the LSB Runtime Environments. For more details, see Section 7.2.

## 10.3 SPECIFICATION MODULE DESCRIPTIONS

*A specification module* is a unique collection of one or more functions that have value for a certain group of runtime implementations. To borrow a business term, a specification module is specific to a “vertical market.” Specification modules can range from informal concepts to certified standards. Product standards contain one or more of the following specification modules.

**LSB-Core** Is a set of interfaces for developers targeting any general purpose Linux runtime. This includes only the basics for runtime environments.

**LSB-Graphics** Provides graphics interfaces such as the X Window System libraries and the OpenGL library. It is to be used in conjunction with the LSB-Core module.

**LSB-Embedded** Is minimal set of interfaces that a developer targeting an embedded system would expect to be able to find. This specification module is not currently included in any product standard, but can be added to one if there is demand. In addition, this module currently includes some things that may not be present in a version used for a product standard.

**LSB-Open118N** Provides additional internationalization commands and interfaces beyond what is included in the LSB-Core. It is to be used in conjunction with the LSB-Core module.

## 10.4 FUNCTIONAL AREA DESCRIPTIONS

A *functional area* corresponds to the smallest standards unit with reasonable justification for individual existence. To divide it into smaller units would not make sense since implementors of that interface would implement all the smaller units anyway. Often the justification for a functional area will be the possibility that it will be useful for implementors who are targeting only some portions of the available standards in an *a la carte* manner.

**Executable and Linking Format (ELF)** Is the definition of the executable files produced by the C compilation system.

**Execution Environment** Consists of the filesystem hierarchy, minimal granted directory and file permissions, recommendations for applications on ownership and permissions, regular expression localization, filename globbing localization, and miscellaneous API behaviors.

**Base Libraries** Consists of libc, libm, libpthread, libgcc_s, libdl, libcrypt, libpm, and libstdcxx.

**Utility Libraries** Consists of libz, libncurses, and libutil.

**System Initialization** Consists of `cron` jobs, init script actions, installation, and removal of `init.d` files.

**Packaging** Consists of the RPM file format, script restrictions, package naming, package dependencies, and package architecture considerations.

**Graphics** Consists of **libX11**, **libXext**, **libSM**, **libICE**, **libXt**, and **libGL**.

## 10.5 SPECIFICATION AMALGAMATION

Figure 10.1 is a visual representation of the new structure of the LSB. Each box represents a functional area. Functional areas are grouped according to the workgroup that maintains them: ELF, FHS, LSB, or Desktop. Functional areas are stacked according to their dependencies. The dimension arrows indicate what functional areas in the stack are included in a specification module.

Product standards, such as the LSB Runtime Environment, contain one or more specification modules such as the LSB-Core.

![](img/d75cffbcb54aabfb0f9854162061d394_154_0.png)

## 10.6 EXPANDING THE LSB WRITTEN SPECIFICATION

Below are some of the acceptance criteria taken from Section 8.2 for publishing or revising an LSB Written Specification.

- The candidate must represent the “best practice” in the development community for the problem it solves. It needs to have emerged as a clear de facto standard and be available on most (or all) of the major distributions.
- The upstream maintainers must be committed to backwards compatibility (for some defined version) and stability. They should be willing to work with developers and distributors on providing a standard everyone can agree on and adopt.
- The upstream maintainers, distributions, and developers should be synced up on compatible versions. If not, they should be willing to agree on and adopt compatible versions.
- If the distributions maintain any patches against the component, these could be merged upstream or dropped. Since the LSB is a behavioral standard, this is not required but could make things easier.

Explicitly check the upstream support; a checklist item for supporting a new architecture should be an explicit check of the upstream components to ensure that the correct symbol versions are specified.

A validation step must be completed prior to a specification being approved by the LSB workgroup. This validation step consists of the completion of all components of the LSB Written Specification, Test Suites, Development Environment, Sample Implementation, and Application Battery. Our process is a closed loop when all of these components are in place.

Multiple implementations should exist and have been used in the validation step. If only a single implementation exists, then the LSB is not really needed, since no compatibility problem can exist. The LSB brand is intended for use by multiple vendors and distributions, and not as a marketing tool for a single vendor or distribution.

## 10.7 Downloading the LSB Written Specification

To obtain the LSB Written Specification go to the LSB Download Web page.¹ You can obtain the specifications in Adobe Portable Document Format (.pdf), RichText Format (.rtf), text (.txt), or line-numbered text (lines .txt). Table 10.1 represents the information that can be accessed via the World Wide Web.

Table 10.1: LSB Written Specification Modules

| Document | Version |
|---|---|
| LSB-Core | 2.0 |
| LSB-Core-AMD64 | 2.0 |
| LSB-Core-IA32 | 2.0 |
| LSB-Core-IA64 | 2.0 |
| LSB-Core-PPC32 | 2.0 |
| LSB-Core-PPC64 | 2.0 |
| LSB-Core-S390 | 2.0 |
| LSB-Core-S390X | 2.0 |
| LSB-Embedded | 2.0 |
| LSB-Graphics | 2.0 |

## CHAPTER ELEVEN

## Using the LSB Test Suites

This chapter describes the LSB Test Suites, how to obtain them, how to use them, and how to add more conformance tests.

### 11.1 UNDERSTANDING THE LSB TEST SUITES

The LSB Test Suites are a family of test suites for testing various aspects of the LSB. They include tests supplied in RPM format for testing LSB Runtime Environments for conformance to the LSB Written Specification. The tests are built in the LSB Development Environment to ensure they are LSB-conformant.

The test suites include both TET-based and non-TET-based tests. The Test Environment Toolkit (TET) is a framework and application program interface for test generation. The following sections describes each test.

#### 11.1.1 TET-Based Tests

##### 11.1.1.1 lsb-runtime-test

This test program is made up of a number of separate test modules combined into a single binary RPM.

POSIX.1-1990 test suite Runtime tests for compliance against the POSIX.1-1990 standard.
