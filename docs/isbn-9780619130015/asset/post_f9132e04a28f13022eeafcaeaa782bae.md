
You have successfully created the Web page for Dominion Consulting by using your knowledge of Perl programming.

## SUMMARY

- An HTML document contains two parts: a head and a body. The head contains the title, which appears on the top bar of your browser window. The body defines what appears within the browser window.
- CGI (Common Gateway Interface) is a protocol or set of rules governing how browsers and servers communicate. Any script that sends or receives information from a server needs to follow the standards specified by CGI.
- To run your Web pages, you need to be in X-Window and have access to a Web browser such as Netscape Communicator and a Web server such as Apache. Using UNIX, you can also test your Web pages using the localhost feature.

## REVIEW QUESTIONS

1. True or False: HTML tags are special codes enclosed in square brackets ([]) .
2. True or False: Most tags are used in pairs: one marks the beginning of a section while a corresponding tag marks the end of a section.
3. Which section of an HTML document contains the title?
   a. HEAD
   b. BODY
   c. PARAGRAPH
   d. BLOCKQUOTE
4. Text between the _________________________ tags appears centered.
   a. [CENTER] and [/CENTER]
   b. <CENTER> and </CENTER>
   c. <ALIGN=center> and </ALIGN>
   d. <JUSTIFY=center> and </JUSTIFY>
5. To run Netscape in UNIX or Linux, you ________________________.
   a. need not be in X-Window
   b. should be in X-Window
   c. must be in X-Window
   d. must have the Apache server installed
6. A basic HTML document has a ________________________.
   a. head and a body
   b. title and a body
   c. set of tags
   d. link to other Web pages
7. The ____________ button in an HTML script is used to transfer the data to a Web server that passes it to a CGI script.
   a. Transfer
   b. Accept
   c. Go
   d. Submit
8. Which of the following is not true?
   a. Perl is the most commonly used CGI programming language.
   b. Perl is the only language used for CGI programming.
   c. CGI scripts do not require any language other than .cgi scripts.
   d. Perl CGI scripts are invoked by Web pages.
9. In Perl, the ______________ character precedes an array variable name.
   a. $
   b. #
   c. %
   d. @

## EXERCISES

1. Create a personal Web page with your name, address, telephone number, and a brief paragraph describing your hobbies and interests. Your name should be centered in a large heading.
2. Design a Web page that allows the user to enter his or her age. The page should have a Submit button that, when clicked, invokes a CGI script. The script should display the user's age in days. (Don't worry about leap years.)
3. Design a Web page that allows the user to enter the width and length of a rectangle. The page should have a Submit button that, when clicked, invokes a CGI script. The script should display the area of the rectangle (width × length).

## DISCOVERY EXERCISES

1. Create an HTML and CGI Perl script to create an interactive Web page to accept your first and last name in the HTML file and pass it to the CGI Perl script, where it displays, "Hello," followed by your first and last name.
2. Create a Perl program to read both the students file and the number list file. Display the students' names in alphabetical order. Display the numbers in the order in which they were read.
3. Design a Web page that is a simple addition calculator. It should allow the user to enter two values. When the user clicks a Submit button, a CGI script returns the sum of the two numbers.

# Developing UNIX Applications in C and C++

## CHAPTER 10

**case**

Dominion Consulting's customers are becoming more conscious of computer security. The programming staff is answering an increasing number of questions about data privacy and protection. Your supervisor asks you to write a simple program that can demonstrate how file encryption and decryption works. (**File encryption** is an operation that scrambles a file's contents into a secret code. A **decryption** operation restores the file to its original state.)

## LESSON A

### objectives

In this lesson you will:

- Create simple C programs
- Use the make utility to revise and maintain source files
- Identify program errors and fix them
- Create a complete C programming application

## C Language Programming

In this chapter, you learn not only how to write C programs, but also how to use other software development tools, such as the make utility. The **make utility** is a UNIX program that controls compilation as you make changes and additions to the programs as they are being developed. Finally, you also write simple C++ programs, so you can understand how C++ programming differs from C programming.

## Introducing C Programming

C is the language in which UNIX was developed and refined. The original UNIX operating system was written in assembly language. **Assembly language** is a low-level language that provides maximum access to all the computer's devices, both internal and external. However, assembly language requires more coding and a greater in-depth treatment of all internal control items. The C language was partly developed to resolve the more lengthy requirements of assembly language. It has drastically reduced these requirements to a high-level set of easy-to-understand instructions. Dennis Ritchie and Brian Kernighan, two Bell Lab employees, rewrote most of UNIX using C in the early 1970s.

Note: Ken Thompson, another Bell Lab employee, also deserves credit for his influence on the development of C. He wrote a forerunner of C, called B, in 1970 for the first UNIX system to run on the DEC PDP-7 mini-computer.

Since its inception, the C language has evolved from its original design as an operating system language to its current status as a major tool in the development of any high-performance application for general use. Since C is native to UNIX, it works best as a UNIX application development tool, where the operating system views the application as an extension of its core functionality. For example, daemons (specialized system process that run in the background) are written in C. They access the UNIX system code just as any other part of the operating system.

C programming may be described, in a nutshell, as a language that uses relatively small, isolated functions to break down large complex tasks into small and easily resolved subtasks. This function-oriented design allows programmers to create their own program functions to interact with the predefined system functions to create powerful and comprehensive solutions to the largest of applications.

Using C to write a program for Dominion's security demonstration is a good choice. Because C is a compiled language, the program source code cannot be viewed. Before you begin to write this program, however, you first need to learn the basics of C programming.

## Creating a C Program

A C program consists of separate bodies of code, known as **functions**. In other languages, bodies of code have different names, such as subroutines or procedures. Each of these bodies of code is designed so it contributes to the execution of a single task. You put together a collection of these functions, and they become a program. Within the program the functions call each other as needed and work to solve the problem for which the program was originally designed.

Creating a program is never done in a single step. As a programmer, you complete many phases before the program is ready to run. The first phase is to create the source code of the program. As with shell scripts and Perl programs, you use a text editor, such as vi or Emacs, to create C programs.

The next phase is to execute the preprocessor and compiler. The **preprocessor** makes modifications to your program, such as including the contents of other files and creating constant values. After the preprocessor prepares your program, the **compiler** executes. The compiler is a program that translates the source code into **object code**, which consists of binary instructions. If you made errors, the compiler locates many of them. When this happens, you use the text editor to correct the errors and recompile the program.

Many compilers translate source code into assembly code. This requires that an **assembler** be invoked to translate the assembly code into object code. The compiler usually invokes the assembler automatically, so you do not need to enter additional commands. Some compilers translate directly from source code into object code, skipping the assembly step. Whatever type of compiler you use, the outcome of this phase is the creation of a file that contains object code.

The final phase requires the use of another tool called a **linker**. This program links all the object files that belong to the program, along with any library functions the program may use. The result is an **executable file**. The entire process is depicted in Figure 10-1.

## C Key Words

The C language, like all programming languages, includes **key words**. These key words have special meanings, so you cannot use them as names for variables or functions. Table 10-1 lists C key words.
