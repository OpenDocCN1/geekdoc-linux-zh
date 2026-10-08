+   3. For a particular build, go to the Tool Settings for the C/C++ Build -> Settings property page and specify the names of the Intel MKL libraries to link with your application, for example, mkl_solver_lp64 and mkl_core (compilers require library names rather than file names, so may omit the "lib" prefix and "a" extension). To learn how to choose the libraries, see Selecting Libraries to Link. The name of the property setting where libraries are specified depends upon the compiler integration.

Note that the compiler/linker will automatically pick up the include and library paths only if the automatic makefile generation is turned on; if not, specify the include and library paths directly in the makefile.

# # Configuring the Eclipse** IDE CDT 3.x

To eclipse CDT 3.x to link with Intel MKL, follow the instructions below:

+   * For Standard Make projects:

+   1. Go to C/C++ Include Paths and Symbols property page and set the Intel MKL include path to <mkl directory>/include.

+   2. Go to the Tabs of the C/C++ Project property page and set the Intel MKL libraries to link with your applications, for example, <mkl directory>/lib/64t/lmkl_intel_lp64.a, <mkl directory>/lib/64t/lmkl_intel_thread.a, and <mkl directory>/lib/64t/lmkl_core.a.

To learn how to choose the libraries, see Selecting Libraries to Link.

Note that with the Standard Make, the above settings are needed for the CDT internal functionality only. The compiler/linker not automatically pick up these settings and you will still have to specify them in the makefile.

+   * For Managed projects, you can specify settings for a particular build. To do this:

+   1. Go to the Tool Settings for the C/C++ Build page. All the settings you need to specify are on this page. Names of the particular settings depend upon compiler integration and are therefore not given.

+   2. If the compiler integration supports path options, set the Intel MKL include path to <mkl directory>/include.

+   3. If the compiler integration supports library path options, set a path to the MKL libraries for the target architecture, such as <mkl directory>/lib/64t.

+   4. Specify the names of the Intel MKL libraries to link with your application, for example, mkl_solver_lp64 and mkl_core (compilers require library names rather than library file names, so omit the "lib" prefix and "a" extension). To learn how to choose the libraries, see Selecting Libraries to Link.