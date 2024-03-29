# Electronic calculators

Doing Arithmetic in our head is boring, error prone, and takes a long time if we're doing a lot of math calculations. Because of this we humans have tried to make devices throughout history that can do Arithmetic for us and let us focus on more important things.

Many mechanical devices were made over time to help with arithmetic, from the [Abacus](https://en.wikipedia.org/wiki/Abacus) to [mechanical calculators](https://en.wikipedia.org/wiki/Mechanical_calculator), and even the [Difference engine](https://en.wikipedia.org/wiki/Difference_engine). But things changed when electricity entered the scene. Travelling at the speed of light meant that electronic calculators would be so fast they'd be able to crunch out numbers near-instantly. The components used in electrical machines were also often much smaller and cheaper than the mechanical equivalents. The only issue stopping people from making electronic calculators was how to make electricity do calculations.

You need to somehow assign numbers to levels of electricity to make an Electronic Calculator. The simplest way to do this is to assign 1 to the presence of high voltage electricity[^1], and 0 to the absence of electricity. This lets us make cheap electronic processors that are as small as possible without worrying without the limits of electrical engineering getting in the way and disrupting our operations<footnote:Signal waves from things like a wifi router, microwaves, antennas etc can cause small changes in the voltage of wires. This is called noise. Encoding 1 to 5.0v and 0 to 0.0v lets us neutralize the effect of noise because the actual voltage of a wire can be rounded to the nearest value (0 or 5) easily. 

The 0s and 1s of electricity are all we need to perform math calculations. We make this possible by encoding normal numbers into binary numbers and math operations into a series of Boolean logic operations.

[^1]: usually 5.0V https://en.wikipedia.org/wiki/Abacus
