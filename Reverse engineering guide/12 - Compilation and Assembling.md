# Compilation and Assembly
To run code written in a programming language it has to be converted to machine code. There are two main ways of doing this:

- Whenever the program is running, convert every line or couple of lines of the source code into machine code (called "interpretation" or "Just-In-Time compilation" (JIT))
- Before running the program, go over the source code and convert all of it to machine code ("Ahead of Time compilation" or "AOT" or just "Compilation")

JIT has the benefit of the code being easy to reverse engineer, and that the code is easier to port to multiple platforms. However it can be slower.
AOT on the other hand takes some time to compile applications but they executing them ends up faster.

Languages like Java, Dart and C# have you compile your code into an executable that runs in a "Virtual Machine" for JITing/Interpreting the code. This Virtual Machine is JVM for java, DVM for Dart, and .NET runtime for C#. 
Applications written in these languages are easy to reverse engineer because often you have full access to all the information about the code.

For AOT compiled languages like C or C++ however lots of information about the code (like structs and variable/function names) are usually removed during compilation to assembly to speed up execution time. You can prevent this by compiling "Debug symbols" alongside your application (producing .pdb files or DWARF information or similar) but once most applications release to the public they don't have any of this symbol info.


The building of applications in AOT compiled languages usually involves 3 steps:

1 - Compilation : Turning source code into equivalent Assembly code (losing information in the process)
2 - Assembling : Converting the assembly into machine code
3 - Linkage : Concatenating the machine code version of all source code files together to produce a single executable

Compilation is done by **Compilers**, Assembling is done by **Assemblers**, and Linkage is done by **Linkers**. These three tools usually ship in the same toolchain to enable easier integration into an app building pipeline.

Most mainstream compilers have the ability to skip stage 2 by directly compiling source code into machine code.
