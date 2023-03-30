# Chapter 7: Stack vs Heap vs Program data segments

Programs use three ways to store data in memory:

1. Allocate random parts of memory to storing data, and store the data there. This forms a **Heap** of data that the program can manipulate any way it wants.

2. Stack the data on top of each other, forming a **Stack** in memory.

3. Store the data in dedicated data segments in the program (right after all instructions).

4. Store the data between instructions.

Stacks are used for storing function parameters and local variables while Heaps are used for anything that doesn't have a fixed size and needs dynamic allocation (such as arrays and linked lists). Global variables and global constants are stored in dedicated segments of the program itself.  Local constants are stored between instructions that use them.
