
## IF Statement
Most languages include the IF statement. In the IF-THEN statement, the expression is evaluated, and if the value is *true*, then Statement<sub>1</sub> is executed next. If the value is *false*, then the statement after the IF statement is the next one to execute. The IF-THEN-ELSE statement is similar, except that specific true and false options are given to execute next. After executing either the *THEN* or *ELSE* part, the statement following the IF statement is the next one to execute.

The usual looping constructs are the *WHILE* statement and the *REPEAT* statement. Although only one is necessary, languages usually have both.

*Inheritance* is the third major form of execution sequencing. In this case, information is passed automatically between program segments. This is the basis for the models used in the object-oriented languages C++ and Java.

Inheritance involves the concept of a *class* object. There are integer class objects, string class objects, file class objects, and so forth. Data objects are instances of these class objects. Objects inherit the properties of the objects from which they were *created*. Thus, if an integer object were designed with the methods (that is, functions) of addition and subtraction, each instance of an integer object would inherit those same functions. One would only need to develop these operations once and then the functionality would pass on to the derived object.

All objects are derived from one master object called *Object*. An *Object* is the parent class of objects such as *magnitude*, *collection*, and *stream*. *Magnitude* now is the parent of objects that have values, such as *numbers*, *characters*, and *dates*. *Collections* can be ordered collections such as an *array* or an unordered collection such as a *set*. *Streams* are the parent objects of *files*. From this structure an entire class hierarchy can be developed.

If we developed a method for one object (for example, *print* method for *object*), then this method *gets* inherited to all objects derived from that object. Therefore, one need not create a new class of integer that, for example, represents the number of days in a year (from 1 to 366), but this new integer-like object will inherit all of the properties of integers, including the methods to add, subtract, and print values. This new concept has been built into C++, Java, and current object-oriented languages.

Once we build concepts around a class definition, we have a separate *package* of functions that are self-contained. We are able to sell that *package* as a product that users may be willing to pay for rather than develop themselves. This leads to an economic model where companies can *build* add-ons for existing software, each add-on consisting of a set of class definitions that becomes inherited by the parent class. See OBJECT-ORIENTED PROGRAMMING.

## Current Programming Language Models
C was developed at AT&T Bell Laboratories during the early 1970s. At the time, Ken Thompson was developing the UNIX operating system. Rather than using machine or assembly language as in (2) or (3) to write the system, he wanted a high-level language. See OPERATING SYSTEM.

C has a structure like FORTRAN. A C program consists of several *procedures*, each consisting of several *statements*, that include the IF, WHILE, and FOR statements. However, since the goal was to develop operating systems, a primary focus of C was to include operations that allow the programmer access to the underlying hardware of the computer. C includes a large number of operators to manipulate machine language data in the computer, and includes a strong dependence on reference variables so that C programs are able to manipulate the addressing hardware of the machine.

C++ was developed in the early 1980s as an extension to C by Bjarne Stroustrup at AT&T Bell Labs. Each C++ class would include a *record declaration* as well as a set of *associated functions*. In addition, an *inheritance mechanism* was included in order to provide for a class hierarchy for any program.

By the early 1990s, the World Wide Web was becoming a significant force in the computing community, and web browsers were becoming ubiquitous. However, for security reasons, the browser was designed with the limitation that it could not affect the disk storage of the machine it was running on. All compute operations that a web page performed were carried out on the web server accessed by *web address* (its Uniform Resource Locator, or URL). That was to prevent web pages from installing viruses on user machines or accidentally (or intentionally) destroying the disk storage of the user.

Java bears a strong similarity to C++, but has eliminated many of the problems of C++. The three major features addressed by Java are:

- 1. There are no *reference variables*, thus no way to explicitly reference specific memory locations. Storage is still allocated by creating new class objects, but this is implicit in the language, not explicit.
- 2. There is no *procedure call* statement; however, one can invoke a procedure using the *member of class operator*. A call to *CreateAddress* for class *address* would be encoded as *address.CreateAddress()*.
- 3. A large class library exists for creating web-based objects. The Java *bytecode* can be transmitted from a web server to the client web site and then *executed*. This saves transmission time as the executing *applet* is on the user’s machine once it is downloaded, and it *frees* machine time on the server so it can process more web “hits” effectively. See *CLIENT-SERVER SYSTEM*.

Visual Basic, first released in 1991, grew out of Microsoft’s GW-BASIC, a product that dates back to the 1980s. The language was organized around a series of *events*. Each time an event happened (for example, mouse click, pulling down a menu), the program would respond with a *procedure* associated with that event. Execution happens in an *asynchronous* manner.

Although Prolog development began in 1970, its use did not spread until the 1980s. Prolog represents a very different model of program execution, and depends on the resolution principle and satisfaction of Horn clauses of Robert A. Kowalski of the University of Edinburgh. That is, a *Prolog* statement of the form *p:: q, r* which means *p is true if both q is true or r is true*. A Prolog program consists of a series of Horn clauses, each being a sequence of relations concerning data in a database. Execution proceeds sequentially through these clauses. Each relation can invoke another Horn clause to be satisfied. Evaluation of a relation is similar to returning a procedure value in imperative languages such as C or C++.

Unlike the other languages mentioned, Prolog is not a complete language. That means there are algorithms that cannot be programmed in Prolog. However, for problems that are amenable for searching large databases, Prolog is an efficient mechanism for describing those algorithms. See SOFTWARE; SOFTWARE ENGINEERING. [M.Z.]

## Progression (mathematics)
Ordered, countable sets of numbers, $x_{1}$, $x_{2}$, $x_{3}$ . . ., not necessarily all different. In general such sets are called *sequences*, whereas the term progression is usually confined to the special types: the arithmetic, in which the difference $x_{i}-x_{i-1}$ between successive terms is constant; the geometric, in which the ratio $x_{i}/x_{i-1}$ is constant; and the harmonic, in which the reciprocals of the terms are in arithmetic progression.

If the first term of an arithmetic progression is *a* and the common difference *b*, then the terms of the progression are given by Eqs. (1). The sum of the first *n* terms $S_{n}$ is given by Eq. (2).

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1792_0.png)

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1792_1.png)

If the first term of a geometric progression is $a$ and the common ratio is $r$, then the terms of the progression are given by Eqs. (3). Excluding the case $r=1$ (when all terms are the same), the sum $S_n$ of the first $n$ terms is given by Eq. (4).

$x_1=a, x_2=ar, x_3=ar^2, \cdots, x_n=ar^{n-1},\cdots$ (3)

$S_n=a\frac{1-r^n}{1-r}$ (4)

The arithmetic mean $A$ and the geometric mean $G$ of $n$ positive numbers are defined by Eqs. (5) and (6).

$A=\frac{x_1+x_2+\cdots+x_n}{n}$ (5)

$G=\sqrt[n]{x_1x_2\cdots x_n}$ (6)

The reciprocals of a sequence (1) form a harmonic progression. There is no compact expression for the sum of $n$ terms. If $x_1$, $x_2$, $x_3$ are in harmonic progression, then Eq. (7) is called their harmonic mean.

$x_2=\frac{2x_1x_3}{x_1+x_3}$ (7) [L.B.]

## Projective geometry
A geometry that investigates those properties of figures that are unchanged (invariant) when the figures are projected from a point to a line or plane. Two features of plane projective geometry are (1) introduction of an ideal line that each ordinary line $g$ intersects (the intersection being common to all lines parallel to $g$), and (2) the principle of duality, according to which any statement that is obtained from a valid one (theorem) by substituting for each concept involved, its dual, is also valid. (“Line” and “point” are dual, “connecting two points by a line” is dual to “intersecting two lines,” and so on.) The subject has been developed both synthetically (as a logical consequence of a set of postulates) and analytically (by the introduction of coordinates and the application of algebraic processes). See CONFORMAL MAPPING; EUCLIDEAN GEOMETRY. [L.M.B.]

## Protozoa
A group of predominantly unicellular microorganisms or infectious agents of cells (the viruses), lacking nuclei, and having asexual and chromosomal reproduction and multidirectional recombination. The Protozoa may be considered to include a kingdom for viruses, although such “organisms” are considered acellular or noncellular (even nonliving) by many authorities, and one for the typical moneran forms, the many kinds of bacteria plus the cyanobacteria (the blue-green algae) and the Pichlorophyceae. See VIRUS.

Bacteria, viruses, and blue-green algae possess little in common, besides such superficial characters as microscopic (or ultramicroscopic) size and frequent involvement in causing diseases in other organisms, including human beings, and such negative characters as not being eukaryotic, not possessing any mouth opening, and not being multicellular (or, in the case of viruses, even cellular). In the smallest dimension, protozoa measure from 0.2 to 10 micrometers; viruses show a diameter of 10 to 300 nanometers, the largest, therefore, just barely overlapping in width with the smallest bacterium.

Monerans (above the virus level) are generally solitary, unicellular forms; but some species are filamentous, colonial, or mycelial. Some are also motile, either by gliding or by the action of bacterial flagella containing the protein flagellin. Modes of nutrition are diverse: absorptive, chemosynthetic, photoheterotrophic, and photoautotrophic. Respiration is anaerobic or aerobic, or facultatively either one. Respiratory and photosynthetic functions are both generally associated with the plasma-membrane system; there are no specialized organelles such as mitochondria or plastids, although thylakoids are present in cyanobacteria and in Pichlorophyceae.

Virus particles can survive in a dried, crystalline, metabolically inert state. Bacteria may produce endospores of great resistance to a variety of environmental stresses; the trophic forms occur ubiquitously in aquatic or moist habitats, including cells and tissues of hosts belonging to all other groups of organisms. Complex viruses have an envelope surrounding the nucleocapsid; many bacteria possess rigid cell walls, and some produce outer sheaths. See ALGAE; BACTERIA; CYANOBACTERIA; EUKARYOTES; PROCHLOROPHYCAE. [I.O.C.]

## Promethium
A chemical element, Pm, atomic number 61. Promethium is the “missing” element of the lanthanide rare-earth series. The atomic weight of the most abundant separated radioisotope is 147. See PERIODIC TABLE.

Although a number of scientists have claimed to have discovered this element in nature as a result of observing certain spectral lines, no one has succeeded in isolating element 61 from naturally occurring materials. It is produced artificially in nuclear reactors, since it is one of the products that results from the fission of uranium, thorium, and plutonium.

All the known isotopes are radioactive. Its principal uses are for research involving tracers. Its main application is in the phosphor industry. It has also been used to manufacture thickness gauges and as a nuclear-powered battery in space applications. See RARE-EARTH ELEMENTS. [FH.Sp.]

## Pronghorn
An antelope-like animal, Antilocapra americana, the sole representative of the family Antilocapridae and of uncertain taxonomic affinities. This animal is reputed to be the fastest untamed in North America and is the only hollow-horned ungulate species with branched horns present in both sexes. Like the deer, the pronghorn sheds its horns each fall; the new growth is complete by midsummer.

The pronghorn live in small herds in rather wild, rocky desert country. They feed on cactus, sagebrush, and other vegetation. In late summer, a buck begins to accumulate a harem of about 10 to 15 does. Two young are usually born in the spring after a gestation period of 95 days. Average life-span for a pronghorn is about 8 years. See WILDEBEEST. [C.B.C.]

## Propagator (field theory)
The probability amplitude for a particle to move or propagate to some new point of space and time when its amplitude at some point of origination is known. The propagator occurs as an important part of the probabilities in reactions and interactions in all branches of modern physics. Its properties are best described in the framework of quantum field theory for relativistic particles, where it is written in terms of energy and momentum. Concrete examples for electron-proton and proton-proton scattering are provided in the illustration. The amplitude for these processes contains the propagators for the exchanged photon and meson, which actually specify the dominant part of the probability of each process when the scattering occurs at small angles. In similar fashion, for any electromagnetic process, a propagator for each internal line of the Feynman diagram (each line not connected directly to the outside world) enters the probability amplitude.

![](img/2cf7974cd6027baa297e5cd95d3d6d43_1793_0.png)
