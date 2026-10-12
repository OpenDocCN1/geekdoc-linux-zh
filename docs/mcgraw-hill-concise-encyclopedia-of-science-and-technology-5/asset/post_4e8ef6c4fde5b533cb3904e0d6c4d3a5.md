
## Problem Solving with Analog Computers

1. The problem under study is described with a set of mathematical equations or, when that is not possible, the system configuration and the interrelations of component influences are defined in block-diagram form, with each block described in terms of black-box input-output relationships.

2. Where necessary, the description of the system (equations or system block diagram) is rearranged in a form that may better suit the capabilities of the computer, that is, avoiding duplications or excessive numbers of computational units, or avoiding algebraic (nongraphical) loops.

3. The assembled information is used to sketch out an analog circuit diagram which shows in detail how the computer could be programmed to handle the problem and achieve the objectives of the study.

4. System variables and parameters are then scaled to fall within the operational ranges of the computer. They may require revisions of the analog circuit diagram and choice of computational units.

5. The finalized circuit arrangement is patched on the computer problem board.

6. Numerical values are set up on the attenuators, the initial conditions of the entire system model established, and test values checked.

7. The computer is run to solve the equations or simulate the black boxes so that the resultant values or system responses can be obtained. This gives the initial answers and the "feel" for the system.

8. Multiple runs are made to check the responses for specific sets of parameters and to explore the influences of problem (system) changes, as well as the behavior which results when the system configuration is driven with different forcing functions.

### Hybrid Computers

The accuracy of the calculations on a digital computer can often be increased through double precision techniques and more precise algorithms, but at the expense of extended solution time, due to the computer's serial nature of operation. Also, the more computational steps there are to be done, the longer the digital computer will take to do them. On the other hand, the basic solution speed is very rapid on the analog computer because of its parallel nature, but increasing problem complexity demands larger computer size. Thus, for the analog computer the time remains the same regardless of the complexity of the problem, but the size of the computer required grows with the problem.

Interaction between the user and the computer during the course of any calculation, with the ability to vary parameters during computer runs, is a highly desirable and insight-generating part of computer usage. This hands-on interaction with the computed responses is simple to achieve with analog computers. For digital computers, interaction usually takes place through a computer keyboard terminal, between runs, or in an on-line stop-go mode. An often-utilized system combines the speed and interaction possibilities of an analog computer with the accuracy and programming flexibility of a digital computer. This combination is specifically designed into the hybrid computer.

In a modern analog-hybrid console, the mode switches in the integrators are interfaced with the digital computer to permit fast iterations of dynamic runs under digital computer control. Data flow in many ways and forms between the analog computer with its fast, parallel circuits and the digital computer with its sequential, logic-controlled programs. Special high-speed analog-to-digital and digital-to-analog converters translate between the continuous signal representations of variables in the analog domain and the numerical representations of the digital computer. Control and logic signals are more directly compatible and require only level and timing compatibility. See ANALOG-TO-DIGITAL CONVERTER; BOOLEAN ALGEBRA; DIGITAL-TO-ANALOG CONVERTER.

The programming of hybrid models is a more complex challenge than described above, requiring the user to consider the parallel action of the analog computer interlaced with the step-by-step computations progressing in the digital computer. For example, in simulating the mission of a space vehicle, the capsule control dynamics will typically be handled on the analog computer in continuous form, but interlaced with the digital computer, where the navigational trajectory is calculated. See COMPUTER.

### Analog States

States in neighboring nuclear isobars that have the same total angular momentum, parity, and isotopic spin. They also have nearly identical nuclear structure wave functions except for the transformation of one or more neutrons into an equivalent number of protons, which occupy the same single-particle states as the neutrons. Analog states (or isotopic analog states, IAS) have been observed throughout the periodic table, indicating that isotopic spin is a good quantum number. See ANGULAR MOMENTUM; L-SPIN; NUCLEAR STRUCTURE; PARITY (QUANTUM MECHANICS).

Since the nucleon-nucleon interaction has been found to be approximately charge-independent, it is possible to consider protons and neutrons as representing different charge states of a single particle, that is, a nucleon. Thus, a level (commonly referred to as a parent state) in a nucleus with Z protons and N neutrons can be expected to have an analog in the neighboring isobar with Z + 1 protons and N − 1 neutrons (and the same total number of nucleons, A = Z + N), where the protons can be expected to occupy the same orbits as those in the parent state. The energy difference between the parent and analog states predominantly arises from the increased contribution from the electrostatic Coulomb interaction to the total energy arising from the extra proton in the analog state. From this amount $M_u e_e$ [electrostatic energy] is subtracted the neutron-proton mass difference of 0.782 MeV (energies are given on the atomic mass scale). The agreement between such calculated energies of analog states and their measured values is in general fairly precise but not exact. The reason is that small additional factors influence the level energies, such as electromagnetic effects, a small charge-dependent nuclear interaction, isospin mixing, and nuclear structure effects.

The study of analog states provides important information used to test nuclear theories. For example, the doublet charge-exchange reactions $(\pi^+, \pi^-)$ [where $\pi^+$ and $\pi^-$ represent a pion with positive and negative charge, respectively] have been used to identify double isobaric analog states, that is, analogs in isobars removed by 2 charge units. Such data have been useful for testing various formulas for predicting the relative masses of isobaric multiplets. Single and double charge-exchange reactions following incident pion beam have also been used to investigate resonances built upon analog states. The single-particle structure of parent states can be studied by observing the particle decay of the analog state when the decay residue is in the nuclear continuum. Measurements of the widths of analog states provide information pertaining to their fragmentation, for example, their mixing with states of the same spin and parity but with total isospin lower by one unit. [D.J.Ho]

### Analog-to-Digital Converter

A device for converting the information contained in the value or magnitude of some characteristic of an input signal, compared to a standard or reference, to information in the form of discrete states of a signal, usually with numerical values assigned to the various combinations of discrete states of the signal.

Analog-to-digital (A/D) converters are used to transform analog information, such as audio signals or measurements of physical variables (for example, temperature, force, or shaft rotation) into a form suitable for digital handling, which might involve any of these operations: (1) processing by a computer or by logic circuits, including arithmetic operations, comparison, sorting, ordering, and code conversion, (2) storage until ready for further handling, (3) display in numerical or graphical form, and (4) transmission.

![](img/2cf7974cd6027baa297e5cd95d3d6d43_119_0.png)

If a wide-range analog signal can be converted, with adequate frequency, to an appropriate number of two-level digits, or bits, the digital representation of the signal can be transmitted through a noisy medium without much degradation of the fine structure of the original signal. See COMPUTER GRAPHICS; DATA COMMUNICATIONS; DIGITAL COMPUTER.

Conversion involves quantizing and encoding. Quantizing means partitioning the analog signal range into a number of discrete quanta and determining to which quantum the input signal belongs. Encoding means assigning a unique digital code to each quantum and determining the code that corresponds to the input signal. The most common system is binary, in which there are $2^n$ quanta (where $n$ is some whole number), numbered consecutively; the code is a set of $n$ physical two-valued levels or bits (1 or 0) corresponding to the binary number associated with the signal number.

The illustration shows a typical three-bit binary representation of a range of input signals, partitioned into eight quanta. For example, a signal in the vicinity of 3/8, full scale (between 5/16 and 7/16) will be coded 011 (binary 3). See NUMBER SYSTEMS. [D.H.S.]

## Analysis of Variance

Total variation in experimental data is partitioned into components assignable to specific causes by the analysis of variance. This statistical technique is applicable to data for which (1) effects of sources are additive, (2) uncontrolled or unexplained experimental variations (which are grouped as experimental errors) are independent of other sources of variation, (3) variance of experimental errors is homogeneous, and (4) experimental errors follow a normal distribution. When data depart from these assumptions, one must use extreme care in interpreting the results of an analysis of variance. Statistical tests indicate the contribution of the components to the observed variation. See CONTRIBUTION OF, [R.L.Bir]

## Analytic Geometry

A branch of mathematics in which algebra is applied to the study of geometry; the subject is also called Cartesian geometry. The basis for an algebraic treatment of geometry is provided by the existence of a one-to-one correspondence between the elements, "points," of a directed line $g$, the elements, "numbers," that form the set of all real numbers. Such a correspondence establishes a coordinate system on $g$, and the number corresponding to a point $P$ of $g$ is called its coordinate. The point $O$ of $g$ with coordinate zero is the origin of the coordinate system. A coordinate system on $g$ is Cartesian provided that for each point $P$ of $g$, its coordinate is the directed distance $OP$. Then all points of $g$ on one side of $O$ have positive coordinates (forming the positive half of $g$) and all points on the other side have negative coordinates. The point with coordinate 1 is called the unit point. Since the relation $OP + PQ = OQ$ is clearly valid for each two points $P, Q$ of directed line $g$, then $PQ = OQ - OP = q - p$, where $p$ and $q$ are the coordinates of $P$ and $Q$, respectively.

Choose any two intersecting lines $g_1, g_2$ of the plane, with Cartesian coordinate systems selected on each so that the intersection point has coordinate 0 in each system. To each point $P$ of the plane an ordered pair of numbers $(x,y)$ is attached as coordinates, where $x$ is the coordinate of the point of intersection of $g_1$ with the line through $P$ parallel to $g_2$ and $y$ is the coordinate of the point of intersection of $g_2$ with the line through $P$ parallel to $g_1$. The lines $g_1$ and $g_2$ are called the x-axis and y-axis, respectively. It is usually convenient to take the same scale on each axis; that is, the segments joining the unit points on the two axes to the origin are congruent. The notation $P(x,y)$ denotes a point $P$ with coordinates $(x,y)$. If $\omega$ denotes the angle made by the positive halves of the two axes, and $d$ the distance between points $P_1(x_1,y_1)$ and $P_2(x_2,y_2)$, application of the law of cosines yields

$$
d = \left[ (x_1 - x_2)^2 + (y_1 - y_2)^2 + 2(x_1 - x_2)(y_1 - y_2) \cos \omega \right]^{1/2}
$$

Since $\cos 90^\circ = 0$, this formula is simplified by taking the axes mutually perpendicular. Though it is occasionally useful to employ oblique axes ($\omega \neq 90^\circ$), the simplifications resulting from a rectangular Cartesian coordinate system make it the usual choice. Such a Cartesian coordinate system is assured in the following. Thus, the distance $d$ between $P_1(x_1,y_1)$ and $P_2(x_2,y_2)$ is given by $\left[ (x_1 - x_2)^2 + (y_1 - y_2)^2 \right]^{1/2}$.

The correspondence between the geometric entity "point" and the arithmetic entity "pair of real numbers," upon which plane analytic geometry is based, results in associating with each geometric locus one or more equations that are satisfied by the coordinates of all those (and only those) points forming the locus (equations of the locus), and in associating with each system of equations in the variables $x, y$ (the graph of the equations) those points are determined by the pairs of numbers satisfying the equations. Thus the algebraic method of studying geometry is balanced by a geometric interpretation of algebra. A central problem in analytic geometry is that of finding equations of certain important figures among curves and surfaces. See CURVE FITTING.

By use of the formula for the distance of two points and the definition of a circle, an equation for a circle with center $C(x_0,y_0)$ and radius $r$ ($r \geq 0$) is found to be $(x - x_0)^2 + (y - y_0)^2 = r^2$.

Much of plane analytic geometry deals with a class of curves which (from the way in which they were first studied) are known as conic sections or conics. A conic is the locus of a point $P$ that moves so that its distance from a fixed point $F$ (the focus) is in a constant positive ratio $e$ (the eccentricity) to its distance from a fixed line (the directrix) which is not through $F$. Let $C(0)$ be the coordinates of $F$, $c > 0$, and take the y-axis as the directrix. Then $P(x,y)$ satisfies the equation $(x - c)^2 + y^2 = ex$; that is, $(1-e^2)x^2 + y^2 - 2cx + c^2 = 0$, and it is easily seen that each point whose coordinates satisfy this equation is on the conic. Hence each conic is represented by a second-degree equation in the Cartesian coordinates $(x,y)$. A conic is called a parabola, ellipse, or hyperbola according as $e = 1, e < 1, e > 1$, respectively. See CONIC SECTION.

Let Cartesian coordinate systems be established on each of three pairwise mutually perpendicular lines of 3-space that intersect in $O$, the common origin of the systems. Suppose equal scales and call the lines the x-axis, y-axis, and z-axis. To each point $P$ of space an ordered triple $(x,y,z)$ of real numbers is attached as rectangular Cartesian coordinates, where $x$ is the coordinate of the foot of the perpendicular from $P$ to the x-axis, and $y$ and $z$ are similarly defined. Thus every point of space has unique coordinates, and each ordered triple of real numbers is the coordinates of a point of space. If $d$ denotes the distance between two points $P_1(x_1,y_1,z_1)$ and $P_2(x_2,y_2,z_2)$, then

$$
d = \left[ (x_1 - x_2)^2 + (y_1 - y_2)^2 + (z_1 - z_2)^2 \right]^{1/2}
$$

It follows from the definition of a sphere and the formula for distance between two points that

$$
(x - a)^2 + (y - b)^2 + (z - c)^2 = r^2
$$

is an equation for the sphere with center $(a,b,c)$ and radius $r$, and by completing the squares of the $x, y,$ and $z$ terms in the equation

$$
x^2 + y^2 + z^2 + 2Dx + 2Ey + 2Fz + G = 0
$$
