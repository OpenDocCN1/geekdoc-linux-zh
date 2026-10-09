# CHAPTER TWO

# Ensuring
Binary Compatibility

Binary compatibility is a feature assurance given by an LSB Certified Runtime Environment to an application. You can take advantage of that assurance by using the LSB as guidance when coding your application. This is part of the promise and value of the Linux Standard Base. This chapter explains the concept of binary compatibility and its importance in developing LSB-certified applications. It also describes each step in the process of ensuring binary compatibility and discusses the different source code standards the LSB Written Specification adheres to. Finally, there is a discussion of binary versus source code compatibility.

# 2.1        ILLUSTRATION OF BINARY COMPATIBILITY

Linux inherently has binary compatibility. Without the need to rebuild or port source code from one Linux release or distribution to another, Linux has achieved binary compatibility for a given hardware platform. You only have to build once for each Linux architecture, such as IA32, PowerPC, or Itanium, and then deploy. The LSB has set some rules and guidelines that make this feature practical for applications. The path to shrink-wrapping an LSB application for Linux includes the following steps:

+   • Coding to the portability layer
+   • Using the correct ABIs
+   • Testing with the LSB application checker