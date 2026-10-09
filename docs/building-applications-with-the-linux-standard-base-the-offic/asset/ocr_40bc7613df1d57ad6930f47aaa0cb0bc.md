**Packaging** Consists of the RPM file format, script restrictions, package naming, package dependencies, and package architecture considerations.

**Graphics** Consists of **libX11**, **libXext**, **libSM**, **libICE**, **libXt**, and **libGL**.

# 10.5 SPECIFICATION AMALGAMATION

Figure 10.1 is a visual representation of the new structure of the LSB. Each box represents a functional area. Functional areas are grouped according to the workgroup that maintains them: ELF, FHS, LSB, or Desktop. Functional areas are stacked according to their dependencies. The dimension arrows indicate what functional areas in the stack are included in a specification module.

Product standards, such as the LSB Runtime Environment, contain one or more specification modules such as the LSB-Core.

![](bbox=[0.05, 0.54, 0.95, 0.85])