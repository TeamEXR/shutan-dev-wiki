# Abstracting Away from Machine Code

While we built our processors to work with 0s and 1s, it's really hard to understand what an instruction like "1010 11 1011" does at a first glance. Programs also become very overwhelming to work on if all you're seeing when looking at them is 0s and 1s.

To fix this we can come up with a Macro language for Processor instructions with a syntax like this:

```<opcode><optional modifier> <operand 1 in hex> <operand 2 in hex> <optional place to store the result>```

Using this syntax, "1010 11 1011" becomes "div 10 11" (div stands for divide).

Applying that syntax to all of a program's Machine code greatly increases the readability, and makes us able to see the exact processor instructions the program is made of. 

Additionally we can label important instruction blocks or data in the program then use those labels when writing Branching instructions or referring to the data.

The process of converting labels to direct addresses and macro instructions to machine code is called **Assembling**, the textual representation of Machine code is called **Assembly Code** (asm for short), and the program used to covnert Assembly Code to Machine Code is called **Assembler**. Now that we have the textual form of machine code to work with, we no longer need to worry about the numbers the textual instructions convert into. 

> This is the power of **Abstraction**, helping us offload mental work to programs we can write ourselves.

Another part of our mental load we can let programs take care of is "how to convert complex tasks like displaying images or playing videos to math operations". We can design programming languages with higher levels of abstraction where we can type `play(Video video);` or similar then stop worrying about the math instructions that'll get translated to.
Code written in **High Level Language**s like C or C++ gets converted to Assembly instructions through a process called **Compilation**, and the program that does this is called **Compiler**. 

What enables us to reverse engineer the inner workings of most software is that we have direct access to the machine code said software consists of, both in the case of assets and in the case of Code. We can then convert this Machine Code into Assembly through the process of **Disassembly**, then make a guess of the code that could have generated the Assembly through the process of **Decompilation**. 

The exact details and mechanisms that go into Reverse Engineering a particular software depends on the Processor in question, the Programming Language it was originally written in, the design of the Processor's Assembly, and the exact software in question (Game vs App vs Operating System vs Driver etc).
