# Chapter 1: Numbers for everything

Since the processors inside computers can do almost anything, it's tempting to think that they must be insanely complicated, or outright supernatural in some way. The truth, however, is that they're actually incredibly simple. They are calculators. What enables us to solve any problem with computers isn't their complexity - rather, it's our ability to turn every problem into a set of numbers and math operations, which a calculator can then solve.

At the most basic level, computers only see and work with numbers. Data can be turned into numbers in various ways, such as assigning Red/Green/Blue values to colors or assigning numbers to each letter on a keyboard to form text. These numbers don't mean anything on their own but rather we assign them meanings to make them represent any data we want. This makes them a **Code** for said data. The rules we use to assign meaning to numbers are called **Encoding** or **Format**, while the process of turning data into numbers is called **Coding**. The reverse process, turning numbers back into the original form of data, is called **Decoding**.

If we encode data into numbers any manipulation of said data becomes encoded into math operations. For example to turn a color from red to blue you simply add to the blue value in it's RGB pair and subtract from the red value. This means that we can design special Input/Output devices that encode and decode data, connect them to a calculator, and form a machine that can solve any of our problems as long as they can be turned into math calculations.  

For example, let's say you want to scan a paper and display it on your computer's monitor:

1. The scanner (an input device), scans the picture and encodes it as numbers
2. The numbers are sent to the processor
3. The processor asks the monitor (an output device) what image it's currently displaying, and compares the numbers representing the scanned image and the currently displayed image, manipulating them using math operations.
4. The new numbers (now representing the scanned image in a way the monitor can work with) are sent to the Monitor
5. The Monitor decodes the numbers and displays the scanned image.

Note: All the processor has to do here is take numbers in, run calculations on them, and give the resulting numbers back. This means that anything that can calculate things can be used as a processor, such as a mechanical engine, an electronic chip, or some guy we pay to do the work for us.

Every program and file in a computer consists of numbers the processors can work with. This representation of said programs and data is called **Machine Code**. The Machine Code underlying every program and data in a computer can be viewed easily, letting us decode them and research how they work. This also lets us modify any program by encoding our modifications into machine code and applying the changes to the existing machine code of the program.

But first we need to understand electronic processors work, and the best way to do this is understand how electronic calculators work first.
