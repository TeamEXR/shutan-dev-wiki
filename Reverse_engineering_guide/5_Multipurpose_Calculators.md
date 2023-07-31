# Multipurpose Calculators

We can build specific circuits that run binary math operations and give us the result then implement them in single purpose calculators. But what if we wanted to make a multi-purpose calculator that can do all of the four operations?

We would need a way of switching between the circuits to change the operation the calculator is going to do. Usually this would need a special device like a lever or a bunch of switches. However, we can use the input device we use to feed in the operands and avoid having to make an additional input device. All we need to do is to encode operations as binary numbers:

- 0x00 = addition
- 0x01 = subtraction
- 0x02 = multiplication
- 0x03 = division

Since we assigned meanings to numbers they became a code. And since they represent  instructions the calculator can do they're called **Operation Code** (Opcode for short).

Once we add an interpreter circuit that reads the instructions we put in one byte at a time and switches between instruction circuits accordingly, we have a full fledged calculator that can take in full instructions through a kaypad and give us the result back

Examples of instructions we can run on our Electronic Calculator:

- 0x06 0x01 0x02 (6 - 2)
- 0x03 0x02 0x02 (3 x 2)
- 0x0A 0x03 0x0B (10 / 11)
- 0x0F 0x00 0x0F (15 + 15)

Now our electronic calculator is fine and dandy for single instructions (we can further expand the capabilities by adding circuits for square roots, powering ups, matrix calculations, etc). But it's still not an electronic *computer*. To turn it into one we have to modify it a bit and add some components.
