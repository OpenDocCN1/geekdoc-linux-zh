# References 249

Interestingly, LLVM supports two different methods for profile collection. The first type, which is same as GCC and ICC, instruments the binary build to collect results. The second type, deviates from the typical profile optimization flow, eschews instrumentation and instead allows feedback to be submitted to the compiler from the built perf() infrastructure. For this work, the binary needs to be built with debugging information, and a special tool must be used to convert the output from perf() into something the compiler can parse. In the author's opinion, this is an excellent feature, designed to oblige the binary requirement that has prevented profile guided optimization from obtaining wide usage. As the author authorially waits to see how this functionality will evolve and affect the other compilers.

In order to generate the first, instrument each compiler uses a similar, but unfortunately different, compiler flag. For GCC, the flag is -profile-generate, for LLVM, it is -profile-instr-generate, and for ICC, it is -prof-gen.

After using this, for both building and linking, the resulting binary will generate additional tracing files upon execution. The number, name, and formatting of these tracing files is specific. GCC generates one trace file, ending with a .cdga suffix, per profile file. foo would have a corresponding foo.cdga. On the other hand, ICC and LLVM only generate one trace file, representing the entire trace. ICC trace files end with a .dyn suffix, while LLVM traces with a .profraw suffix.

Once the trace file or files, has collected, a different compiler flag is used to inform the compiler to locate, parse, and utilize them. For GCC, this flag is -profile-instr-use=filename, and for ICC, the flag is -prof-use. The result from built is ready for benchmarking.

# REFERENCES

+   - Free Software Foundation, 2004, GCC(11) Manual Page.
- Gerber, B., Bik, A.J., Smith, K.B., Tian, X., 2006, The Software Optimization Cookbook: High-Performance Recipes for IA-32 Platforms. Intel Press, Hillsboro, OR.
- Intel Corporation, 2013, 10. Intel 64 and IA-32 Architectures Software Developer's Manual. Computer Hardware Manual.
- Intel Corporation, 2014, 10. Intel 64 and IA-32 Architectures Optimization Reference Manual. Order Number: 248966-030.
- Intel Corporation, 2014, 10. C++ Compiler XE User and Reference Guide.
- LLVM Project, 2014, 10. llvm-profdata—Profile Data Tool.
- Patterson, D.A., Hennessy, J.L., 2007, Computer Organization and Design: The Software Interface, third ed. Morgan Kaufmann, Burlington, MA.
- The Clang Team, 2014. Clang: Profile Guided Optimization.