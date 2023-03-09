# Chapter 2: CPUs and Assembly

In Chapter 1 we mentioned how All data is numerical, meaning that things like 3D/2D graphics, Animations, Text, Music, and Input/Output are either numbers or can be turned into numbers. Thus all processing on said data boils down into doing a lot of math operations really fast. This is exactly what **Central Processing Unit**s (CPUs) are designed for.

At a minimum, a CPU needs to do a couple of things:

- Perform math operations on binary numbers 

- Do bit manipulation 

- Load values from memory or store them there

- Jump from one instruction in machine code to another instruction, either conditionally or unconditionally

There are many different ways to translate above instructions to numbers, as well as different ways the CPU could work with memory to optimize executing these instructions. During Computing history this resulted in many different instruction set designs called **Instruction Set Architechture**s. Examples include x86, x64, ARM32, Thumb, and Thumb2. Any operations not in the 4 categories above isn't included in the ISA becuase almost every single operation can be translated to the four operations above with varying degrees of efficiency. 

If the conversion makes the process too inefficient (either by taking too long, not being accurate enough, or using too much power), then specialized processing units are designed to work alongside the main CPU, taking care of these operations. Common examples of calculations handled by these processors include Floating Point Math[1], Digital Signal Processing[2], Graphics[3], Crypto-based Security[4], and AI processing[5]. These Special processors either expand the main CPU's ISA with additional instructions (creating an **ISA Extension**) or they come with their own exotic ISA to further optimize their processing.

With all of that introduction, let's talk about the processors inside Nintendo 3DS, beware of the big scary words!

Nintendo 3DS uses 3 CPUs, one for running 3DS games and HOME menu, one for Running DS games in backwards compatibility mode, one for running GBA games either through the Ambassador's program[5] or through the GBA virtual console. We're mainly concerned with the one running 3DS games as this guide is aimed at reverse engineering 3DS games.

The CPU in question is called ARM11MPCore, it is designed to run Thumb and ARM32 instructions (specifically version 6). It also has a specialized co-processor embedded inside itself for handling floating point calculations (called Vector Floating Point version 2 or VFPv2).  

In addition to the three CPUs there's also a GPU (Graphical Processing Unit) for handling Graphic calculations, and a DSP (Digital Signal Processor) for handling calculations needed while recording or playing Audio.

Here's a simplified diagram of how these components work together: 

<placeholder>

The ARM company has produced manuals for the ARM11MPCore CPU explaining the exact instructions it can run, how it can access memory, the Assembly representation of those instructions (called ARMv6k-Thumb assembly), and other details.

You could read those manuals to get a full sense of every single instruction (in fact here's the link[placeholder]), but they're chuck full of big words and confusing terminology that need a lot of googling to understand.

In the following chapters we'll do a quick deep dive of the instruction set ARM11MPCore and the VFPv2 co-processor inside it can run, then we'll introduce the tools Shutan uses to poke away at the game's Assembly and modify it as needed.
