# Chapter 4: Chaining Operations together

Let's say you want to use a math formular that looks like this:

`(23423 + 11241) / (12341 x 123) x (8172 + 1828)`

We can divide it into a list of instructions and feed it one by one to an electronic calculator:

1. 23423 + 11241

2. 12341 x 123

3. 8172 + 1828

4. Result of 1 / result of 2

5. Result of 4 x result of 3

We could make an instruction scanner for our Calculator, write the 5 instructions above on a paper with a HALT instruction at the end, and feed it to the scanner. The Scanner then would feed each instruction into the Calculator (converting decimal numbers to binary along the way), and stop when it reaches the HALT opcode. However to successfully run the instructions the Calculator would ask us for the result of operations 1 through 4. That is because, unlike us humans that can temporarily store the result of each operation in our head, the Calculator has no **Working Memory** to store the result of each operation.

A working memory is a place that our Calculator can temporarily store data between operations needing said data. We can use an empty area on the same paper the instructions are on for memory, but it's electronically powered memory is both faster and takes less space. All we need to do is build tiny circuits that can each store one bit (called a bit latch[1]) out of logic gates, then put them together to form any amount of memory we want and put it in the Calculator's processor.

For the sake of simplicity we can divide the memory available to our Calculator into equally sized slots called S1, S2, S3, and S4. After reconfiguring our instruction scanner and tweaking operation circuits to be able to store the result of each operation into memory slots, our instructions for the formula above starts looking like this:

1. 23423 + 11241, S1

2. 12341 x 123, S2

3. 8172 + 1828, S3

4. S1 / S2, S4

5. S4 x S3

Voila, now our Calculator can take any amount of instructions chained together and execute them, halting when it runs out of instructions to run.

The idea of instructions chained together is pretty important. We explained in chapter 1 that once everything we want to work with is encoded to numbers, manipulating those things becomes encoded to a chain of math operations Calculators can run. These long chains of instructions representing tasks we want to accomplish are called **Program**s.

Now we have a perfectly working calculator that can cover most of our basic math needs, but this calculator isn't adequate for running various programs given to Computers. Those kinds of programs would need a lot more processing power, better Input/Output devices, a ton more memory, memory usage in a way that's organized and most importantly, they would need a way of implementing conditional execution.

In the next chapters we'll discuss more characteristics that differentiate Computers from Calculators.
