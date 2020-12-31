[Think Stats Chapter 3 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2004.html#toc31) (actual vs. biased)

---

_Something like the class size paradox appears if you survey children and ask how many children are in their family. Families with many children are more likely to appear in your sample, and families with no children have no chance to be in the sample.
Use the NSFG respondent variable ```NUMKDHH``` to construct the actual distribution for the number of children under 18 in the household._

---
First, read in the data...
```
resp = nsfg.ReadFemResp()
```
To create a PMF for the ```NUMKDHH``` variable, first use the Pmf constructor included in the thinkstats2 library to transform the data into a PMF-friendly format where each value associated with the variable is mapped to its probability. 

```
actual_pmf = thinkstats2.Pmf(resp.numkdhh, label = 'actual')
```
The contents of this Pmf object will look like this:
>Pmf({0: 0.466178202276593, 1: 0.21405207379301322, 2: 0.19625801386889966, 3: 0.08713855815779145, 4: 0.025644380478869556, 5: 0.01072877142483318}, 'actual')

Now that the data has been transformed into the appropriate format, plot the PMF using thinkplot.Pmf().

```
thinkplot.Pmf(actual_pmf)
thinkplot.Config(xlabel = 'number of children in household', ylabel = 'PMF')
```
The distribution shows 0 children being the most common value with the probability of a given family size decreasing as family size increases.

![Exercise_3_1_Plot1](https://github.com/emmamcclaire/dsp/blob/master/img/exercise_3_1_plot1.png)

---

_Now compute the biased distribution we would see if we surveyed the children and asked them how many children under 18 (including themselves) are in their household. Plot the actual and biased distributions, and compute their means._

---

To compute the biased distribution, take the actual PMF and multiply the probability associated with each value by the value itself. Note that the PMF needs to be normalized after this operation is done.
> Ex: biased P(2 children) = P(2 children)*2

This can be done using the function defined below. The function is a slightly modified verison of the one included in Chapter 3, which shows what operation is being performed on the Pmf object more explicitly:

```
def BiasPmf(pmf, label):
    new_pmf = pmf.Copy(label = label)
    
    for x, p in pmf.Items():
        new_pmf[x] = p*x
    
    new_pmf.Normalize()
    return new_pmf
```

Now, use the function to create the biased distribution. Then visualize both distributions on the same plot using the thinkplot library.

```
biased_pmf = BiasPmf(actual_pmf, label = 'biased')

thinkplot.PrePlot(2)
thinkplot.Pmfs([actual_pmf, biased_pmf])
thinkplot.Config(xlabel = 'number of children in household', ylabel = 'PMF')
```
Both distributions are now overlaid, showing how the biasing the data has shifted the distribution to look more like a normal distribution.

![Exercise_3_1_Plot2](https://github.com/emmamcclaire/dsp/blob/master/img/exercise_3_1_plot2.png)

Finally, use the Pmf.Mean() function to find and compare the means of each distribution.

```
print('actual mean: ', actual_pmf.Mean(), '\nbiased mean: ',biased_pmf.Mean())
```

actual mean:  1.024205155043831  
biased mean:  2.403679100664282

The actual and biased distributions in this example are very distinct from each other; much more so than in the earlier class size example. It makes sense that this would be the case, though, given that the actual distribution of children in the household shows 0 children as the most frequent value. This means that the most common category of respondents would have no chance to be included in the sample.
