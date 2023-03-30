# Chapter 2.2: Using Boolean Algebra to make electricty do Binary Math

Boolean Algebra is a branch of mathematic where math nerds grab a bunch of "True" and "False" values and do logic operations on them. It's goal is to state every logic question as math functions and solve them using math rules.

How is that any relevant to electronic calculators and computers? The answer is that we can map True/False to electricity/no-electricity just like we did with 1s and 0s. And we can directly map 1s and 0s to True/False respectively.

This way we can describe Binary math operations as a bunch of logic questions put together, and use special devices called Logic Gates to make binary math processors.[1] But what are Logic gates?

## Logic Gates

Logic gates are devices that take two inputs and then give an output based on the logic of the device. For example an OR gate outputs "True" if any of the inputs are "True". An AND gate outputs "True" only if both inputs are "True". We can construct Logic gates that work with electricity, fluids, steam, rotational power, and light. Modern processors are electronic, thus they use logic gates that work with electricity to produce results.

## Using logic gates for Math

Here's how addition works in the decimal system: when we add two numbers together we get the sum of those numbers (in 3 + 4 = 7, 7 is the sum of 3 and 4). but if the result doesn't fit in a digit then we carry the extra value into the next power of 10 (in 5 + 7 = 12, 2 is the sum digit of 12 while 1 is the carry digit)

Same thing applies to Binary math, but the possible outcomes of binary addition are even simpler:

- 0 + 0 = 00 (carry bit 0, sum bit 0)

- 0 + 1 = 01 (carry bit 0, sum bit 1)

- 1 + 0 = 01 (carry bit 0, sum bit 1)

- 1 + 1 = 10 (carry bit 1, sum bit 0)

We can calculate the result of the carry bit using an AND gate, and the result of the sum bit using a XOR gate, essentially splitting the binary addition into two logical operations. Thus we can hook up an AND gate and a XOR gate to the same 2 inputs to calculate the simplest binary addition possible. 

what if we want to add two digit numbers or three digit numbers together? we could define a table for every possible outcome but that'd take too long. Instead we can turn the operation into a chain of single digit additions.

For example 103 + 201 in decimal becomes:

- first addition: 1 + 3 = 4 (carry digit: 0)

- second addition: 0 + 0 + carry digit from first addition(=0) = 0 (carry digit: 0)

- third addition: 1 + 2 + carry digit from second addition(=0) = 3 (carry digit: 0)

- the result is 304.

Thus we can scale up binary addition by chaining binary adders together, each taking care of a single addition.

In fact we could define the other three math operations as a chain of additions and use binary adders chained up together:

- Subtraction is just adding a negative number to a positive number (5 - 3 = 5 + (-3)). We can encode negative binary numbers to some positive binary numbers to accomplish this.[2]

- Multiplication is just an addition chain for an operand (3 x 4 = 3 + 3 + 3 + 3, or 3 x 4 = 4 + 4 + 4)

- Division is counting how many times we can subtract the first operand by the second operand while the result stays 0 or positive.

We can hook up binary adders in configurations that let us do Subtraction, Multiplication, and Division. Making dedicated circuits for each operations.

Then we can hook up Input/Output devices to each circuit, making calculators that can do Addition, calculators that can do subtraction, etc. But creating calculators that can do any of the operations above is a bit more tricky.

[1] You can theoretically design logic math systems with 3 or more values then design logic gates working with said values but the whole design would get so complicated it'd become hard to comprehend in the first place.

[2] The most efficient way to encode negative binary numbers to positive ones is [Two's complement](https://en.wikipedia.org/wiki/Two%27s_complement)
