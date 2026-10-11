Agai*Shell*”). This shell was compatible with the original shell created by Steven R. Bourne, but included many enhancements. It was also compliant with the POSIX standard for shells.

Bash is the standard shell provided with most Linux distributions, including Red Hat, SuSE, Mandrake, Slackware, and UnitedLinux.

# When Is a Program a Shell Script?

A script is similar to a program but there is no formal definition for what constitutes a script. It is a type of simple program, and scripts and programs share many features in common. Linux programmers with few special requirements need advance beyond writing shell scripts.

As shells matured, they gained many features that you might not expect to find in a program designed to schedule commands. Most shells, including Bash, can perform bit manipulation, string processing, and TCP/IP connections. They have typed variables, built-in commands, and user-defined functions. The distinction between shells and programming languages has become blurred.

In general, there are two key differences between shell scripts and more complex programs. First, shells are designed to handle short, simple tasks. They lack the rigid structure and semantic checking of a high-level language. Shell scripts can be written quickly because they assume the programmer knows what he or she is doing, and for short scripts, this is usually true. Second, shells always execute their scripts slowly. Although most shells perform some kind of pre-processing to speed up execution, they still interpret and carry out one line at a time. High-level languages are faster because they almost always translate a program into machine language to gain the full performance.

When tackling any programming problem, it’s essential to choose the right tool for the job. Developing large projects as shell scripts will mean your project will run slowly and be difficult to maintain. Developing scripts in a high-level language will lead to a longer and more costly development time.

# The Necessity of Structured Shell Programming

Shell scripts remain a staple of the business world. With high development costs, it is not practical to develop everything in a high-level language. Many business processes are simply a matter of following a series of steps, after which the results are labeled and archived. This is the very type of activity scripts are made to handle.

Over time, shells have collected new features, often by copying the capabilities of other shells. In his book, The Human*nterfac*, Apple Macintosh interface designer Jef Raskin once spoke with a pilot regarding the design of the plane’s autopilot. The device was designed with five ways to enter coordinates. The reason for this design was to reduce training costs by emulating other autopilots. However, a pilot pointed out that the operator of the aircraft is responsible for knowing how to operate every piece of equipment, and that meant he had to know how to adjust the autopilot in each of the five ways.