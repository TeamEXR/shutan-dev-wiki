# Looping and Conditions

There's two things programs can do that our processor isn't capable of yet: loops and if-else blocks. Let's implement those.

To implement loops we need to add a special opcode to our processor that makes it change the current line of the program it's currently executing, essentially "jumping" to a different part of the program. In most processors this opcode is called **Branch** because the execution branches out of how the execution would normally go.

To implement conditional execution we need a way to evaluate conditions in the first place. On most CPUs this is made possible by making a special "compare" opcode, storing the result in a register, then adding versions of the Branching opcode which only gets executed based on the number in that register.

Here's how we can use the new opcodes:

1. **Loops**: We can write a block of the program starting at Line A and ending at Line B that keeps looping until a specific condition is met. The way we do this is by putting "Branch-If-Condition-Not-Met A" at Line B, instructing the processor to jump to line A and execute every single instruction between Line A and Line B again. 
2. **If-Else Blocks:** We implement this by evaluating a condition in our program then Branching to the part of the program we want to execute if the condition is met. Otherwise we'll branch to the part of the program we want to execute if the condition isn't met.

We'll see actual examples of what the above strategies look like in code in the advanced RE guide but suffice to say, branching execution and conditional execution are pretty important. They make computers able to do even more complex tasks.
