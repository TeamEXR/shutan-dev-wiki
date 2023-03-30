# Chapter 2.1: Numeral Systems

In chapter 1 we said that numbers in a computer don't mean anything until we assign them meanings. This is true for numbers in everyday usage as well. They are in essence symbols we use when counting and talking about the count of irl things like apples, oranges, computers, calculators, etc. Thus numbers in general are a Code. But to explain the encoding of everyday numbers we need to go back to Elementary School math.

In elementary school, we were told that every number consists of digits, and valid digits were 0 1 2 3 4 5 6 7 8 9. We were then told that we can represent values higher than 9 by putting these digits together, the value of the resulting number would depending on which digit is placed where. For example 10 has a higher value than 01 becasue the digit 1 is put to the left-most "slot" in the number (making it the most significant digit).

There's a simpler way to express that concept, we can use powers of 10 to show the worth of each digit in a single number. Each digit's worth is the digit itself multiplied by 10 to the power of the slot number it's in. For example:

- 15 = (1 x 10 ^ 1) + (5 x 10 ^ 0)

- 129 = (1 x 10 ^ 2) + (2 x 10 ^ 1) + (9 x 10 ^ 0)

- 1005 = (1 x 10 ^ 3) + (0 x 10 ^ 2) + (0 x 10 ^ 1) + (5 x 10 ^ 0)

In a number system like this we assign 10 digits (0 1 2 3 4 5 6 7 8 9) specific values, then use powers of 10 to help us assign values bigger than 9 to numbers. This encoding of values to numbers is called **The Base-N Positional System**. Since we use everyday numbers based on powers of 10 the specific encoding for them is called **The Base-10 Positional System**, also known as the **Decimal System**.

The Important point here is that we don't have to use 0 1 2 3 4 5 6 7 8 9 as our symbols, that's a pretty arbitrary rule that was widely accepted because we can count from 1 to 10 with our fingers.

For example, electronic calculators are designed to treat lack of electricity as 0 and high enough voltage as 1. To represent any higher values with those digits we'd need to put them together, using powers of 2 to assign value to each digit. This results in a **Base-2 Positional System**, also known as the **Binary system**. 

Here are the same examples from above, represented in binary:

- 1111 (15 in decimal) = (1 x 2 ^ 3) + (1 x 2 ^ 2) + (1 x 2 ^ 1) + (1 x 2 ^ 0)

- 10000001 (129 in decimal) = (1 x 2 ^ 7) + (0 x 2 ^ 6) + .... + (0 x 2 ^ 1) + (1 x 2 ^ 0)

- 1111101101 (1005 in decimal) = ( 1 x 2 ^ 9) + (1 x 2 ^ 8) + (1 x 2 ^ 7) + (1 x 2 ^ 6) + (1 x 2 ^ 5) + (0 x 2 ^ 4) + (1 x 2 ^ 3) + (1 x 2 ^ 2) + (0 x 2 ^ 1) + (1 x 2 ^ 0)

1111101101 represents the same value as 1005, just with different values assigned to each individual digit. The simplicity of this numeral system will help us later once we explain Boolean Algebra.

Another way we can assign values to numbers is to use 16 digits (0 1 2 3 4 5 6 7 8 9 A B C D E F) and represent any higher value using powers of 16. This results in a **Base-16 Positional System**, also known as the **Hexadecimal System**.

Let's see what the above numbers look like in hexadecimal:

- F (15 in decimal) = (F x 16 ^ 0)

- 81 (129 in decimal) = (8 x 16 ^ 1) + (1 x 16 ^ 0)

- 3ED (1005 in decimal) = (3 x 16 ^ 2) + (E x 16 ^ 1) + (D x 16 ^ 0)

3ED represents the same value as 1005, it's just written in Hexadecimal instead of Decimal.

Note: to easily understand which base different numbers are written in, special prefixes are used with the numbers. "0x" is used for hex numbers (0x15 = 21) while binary numbers use "0b" (0b1111 = 15). Decimal numbers don't use a prefix

We can represent the same value using any arbitrary base, but Binary and Hexadecimal are important ones when it comes to working with calculators and computers. The 0s and 1s we designed our Calculators around earlier are the same digits used in the binary system, and as we'll find out in a bit Hexadecimal numbers are easier to deal with than binary ones when encoding data.

## Bits, Bytes, Words

**Bi**nary Digi**t**s are called Bits. A **Byte** is a common way of splitting binary numbers used in every computer today, consisting of 8 bits. A **Word** is a fixed sized unit containing bits that is important to Processor designs (we'll talk more about Word in the Advanced RE guide as it's not that important here).

Machine Code in every computer is divided into Bytes, but it's pretty common to use the hexadecimal representation of bytes (called **Hex Bytes**) rather than the binary representation. This is possible because 2 hexadecimal digits can contain as many values as 8 bits.

Note: We'll use hex bytes from now on when talking about binary numbers.

With all of that out of the way, let's talk about how we can do math operations using electricity.
