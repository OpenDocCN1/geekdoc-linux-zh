```
linuxbox$ unzip -al nasml097s.zip
```

after copying it to a suitable directory. To build it, you can then copy the appropriate makefile

```
linuxbox$: cp makefile.unx Makefile
```

and run

```
linuxbox$: make
```

# 1.6 Other Assemblers

MASM and Turbo-Assembler are assemblers that have been very widely used in connection with DOS. The fact that Windows is not so easy to work with using assembly language has led to a decrease in the popularity of these assemblers. Many people have the impression that Linux is not particularly assembler-friendly either. This impression is partly based on the view of assembly language that you get working with gcc. Those accustomed to Intel syntax may understandably find the AT&T syntax awkward. Worse, when assembly language instructions are inserted into C code, the quotation marks required by gcc and the line-jumbling that occurs are pretty repellent. I hope that by chapter 7, readers will be persuaded that interacting with Linux using assembly language can be clean and neat.

There are a few other assemblers around. A brief discussion of them can be found in an Assembly-HOWTO at the Linux Documentation Project's Website, www.linux.doc.org/HOWTO.

# Further Reading

*Open Sources,Voices from the Open Source Revolution* ChrisDiBona et. al., O’Reilly: 1999.

*A Quarter Century of Unix,* PeterSalus, Addison-Wesley: 1994.

# Chapter 2. PLACEHOLDING NUMERATION

The ENIAC did not use the binary system. Its arithmetic processor used vacuum tubes wired together into rings, which worked like old desktop adding machine wheels. These were base ten contraptions. Since then, however, all electronic computers have done their arithmetic using the binary system (base two).
Consequently, descriptions of computer arithmetic are customarily expressed using the binary system or related systems such as hexadecimal (base sixteen) or octal (base eight). An understanding of these number systems is essential. Readers already familiar with them may prefer to skip this chapter.

# 2.1 The Decimal and Pental Systems

Before the invention of placeholding decimal notation in the East, probably in India or China, systems of notation built around powers of ten, which were not placeholding systems, were common. The system used by Archimedes, for example, is shown in Table 2.1. In this system, SPA represents the number $171$. Greek letters of course, not Latin letters, were used. The most apparent disadvantage of this kind of system is computational. The notation is no help at all in seeing that

Table 2.1. Non-Placeholding Decimal System

| | | | | | |
|---|---|---|---|---|---|
| A | 1 | J | 10 | S | 100 |
| B | 2 | K | 20 | T | 200 |
| C | 3 | L | 30 | U | 300 |
| D | 4 | M | 40 | V | 400 |
| E | 5 | N | 50 | W | 500 |
| F | 6 | O | 60 | | |
| G | 7 | P | 70 | | |