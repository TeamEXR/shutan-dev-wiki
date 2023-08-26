# Reverse Engineering applications

If creating an application involves compilation, assembling, and linkage then reverse engineering the application would involve going backwards: delinking, disassembling, and decompilation.

Reverse engineering JIT-based applications is relatively easy because no information about the application's source code is lost, therefore all you need to peek into an application's inner workings is a tool to put that information together with the code.
For example to examine C# executables all you need is a tool like DotNetPeek to "decompile" the code, giving you full access.

The Reverse Engineering process is tougher with AOT apps however. This is because a lot of critical information about the app is lost during the process of compilation and linking:
- Function names and variable names are gone
- Structs are decomposed into variables next to each other in memory, this can make it difficult if a variable is part of a struct. and if so, which struct
- Many smaller functions are inlined into larger functions that call them, bloating their size and making the process of reverse engineering annoying
- Because the code from multiple source files is linked together, it's hard to judge what particular source file a function comes from (therefore you can't speculate on what area a function could be part of)
- Class information is lost, therefore it's not easy to judge what class each particular function comes from

These factors combined often result in reverse engineering apps and games becoming annoying and time consuming.

Because of this most Reverse Engineering discussion and activity is usually centered around fighting against malware and finding exploits/hacks rather than fully reverse engineering games to make them moddable.
