of processors can run on any corresponding LSB Certified Runtime Environment.

# ### 2.4 LSB BINARY COMPATIBILITY

*Binary compatibility* is the expectation that a properly-coded application, which executes successfully and correctly on one instantiation of an operating system, will continue to do so on another OS of the same hardware platform. The LSB is dedicated to the idea that Linux-based applications can be portable across Linux operating system distributions. Now that a specification exists that both operating system providers and application developers can agree upon, users are already benefiting from increased compatibility of their applications and tools.

# #### 2.4.1 Binary versus Source Compatibility

Binary compatibility is not the same as source compatibility. A source code fragment that describes the same operation on two instances of an OS can become a binary that will only operate on one of them, even on the same hardware platform. Binary compatibility is a “contract” between the OS and the application; the OS will provide a set of known functions in a specified way, and the application will use those functions and avoid other functions for which there is no specification.

The LSB provides this contract. For the OS, it describes both the set of known functions and the known way of making them available. It does this via its programming interface (API) and binary interface (ABI) documents for each hardware platform. For applications, the LSB offers testing and certification to assure that only the functions provided for by the LSB are used.

# #### 2.4.2 Coding Compatible Applications

Applications using only the LSB-documented interfaces will run unmodified on all LSB-certified OSes for a given hardware architecture family, as described by that LSB ABI specification architecture. Application software that meets this specification and successfully passes testing using the LSB Application