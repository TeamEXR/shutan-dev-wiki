# Chapter 3: Multipurpose Calculators

We can build specific circuits that run binary math operations and give us the result then implement them in single purpose calculators. But what if we wanted to make a multi-purpose calculator that can do all of the four operations?

We would need a way of switching between the circuits to change the operation the calculator is going to do. Usually this would need a special device like a lever or a bunch of switches. However, we can use the input device we use to feed in the operands and avoid having to make an additional input device. All we need to do is to encode operations as binary numbers:

- 00 = addition

- 01 = subtraction

- 10 = multiplication

- 11 = division

Since we assigned meanings to numbers they became a code. And since they represent  instructions the calculator can do they're called **Operation Code** (Opcode for short).

Once we add an interpreter circuit that reads the instructions we put in and switches between instruction circuits accordingly, we have a full fledged calculator that can take in full instructions through a kaypad and give us the result back

Examples of instructions we can run on our Electronic Calculator:

- 110 01 10 (6 - 2)

- 11 10 10 (3 x 2)

- 1010 11 1011 (10 / 11)

- 1111 00 1111 (15 + 15)

Now our electronic calculator is fine and dandy for single instructions (we can further expand the capabilities by adding circuits for square roots, powering ups, matrix calculations, etc). But it's still not an electronic *computer*. To turn it into one we have to modify it a bit and add some components.
