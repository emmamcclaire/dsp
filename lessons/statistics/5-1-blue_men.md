[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

---

_In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters µ = 178 cm and σ = 7.7 cm for men, and µ = 163 cm and σ = 7.3 cm for women.
In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf._

___

First, create a frozen random variable called using ```scipy.stats.norm``` to represent the normal distribution of heights in the U.S male population where µ = 178 cm and σ = 7.7 cm.

```
mu = 178
sigma = 7.7
dist = scipy.stats.norm(loc=mu, scale=sigma)
```

Next, we want to be able to plug in height values into the cdf function associated with ```dist``` so before we can do that, we need to convert the height from feet to centimeters using the following function: 

```
def feet_to_cm(feet, inches):
    """ convert feet to cm """
    tot_inches = feet*12+inches
    cm = tot_inches*2.54
    return cm

print("5ft 10in: ", feet_to_cm(5, 10),
      '\n 6ft 1in: ', feet_to_cm(6, 1))
```

Now that we know we are looking for the percentage of males between **177.8 cm** and **185.4 cm**, we can use those values to find the percentage of the population with heights <= each value:

```
print(dist.cdf(177.8),
dist.cdf(185.4))
```

To find the percentage of the male population that falls between these heights, we just need to subtract these values from each other.

```
dist.cdf(185.4) - dist.cdf(177.8)
```

The resulting value is **0.34** or **34%**, meaning that approximately 34% of the male U.S. population is between 5'11" and 6'1". This is a large chunk of the population, but the result is expected since the range in question spans almost exactly the same range as the population mean to the first standard deviation in the positive direction, which in a normal distribution, contains 34% of the data.


