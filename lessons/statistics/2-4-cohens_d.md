[Think Stats Chapter 2 Exercise 4](http://greenteapress.com/thinkstats2/html/thinkstats2003.html#toc24) (Cohen's d)

_Using the variable ```totalwgt_lb```, investigate whether first babies are lighter or heavier than others._
_Compute Cohen’s effect size to quantify the difference between the groups. How does it compare to the difference in pregnancy length?_

---
Calculating the means of each group gives an initial sense of the differences in birth weight between the 'firsts' and 'others' groups:

``` 
print('mean first babies: ', firsts.totalwgt_lb.mean(), 
'\nmean other babies: ', others.totalwgt_lb.mean(), 
'\nweight difference between group means (lbs): ', abs(firsts.totalwgt_lb.mean() - others.totalwgt_lb.mean()))
```
  >mean first babies: 7.20  
  >mean second babies: 7.33  
  >weight difference between group means (lbs): 0.12
  

The group means have a difference of 0.12 lbs, but with this information alone, it is difficult to determine how meaningful this weight difference is. Looking at the size of the effect of first vs other births on birth weight using Cohen's d shows a noticeable effect of birth order on birth weight.
```
print("Cohen's d: ", CohenEffectSize(firsts.totalwgt_lb, others.totalwgt_lb))
```
>Cohen's d: -0.09


Comparing this to the Cohen's d value for difference in pregnancy length between first babies and others, which was ```0.03```, it is clear that birth order has a much larger effect on birth weight than on pregnancy length. Interestingly, the effects are working in opposite directions (indicated by the +/- signs for each Cohen's d value): birth weight tends to be lower in first pregnancies, while length of pregnancy tends to be higher in first pregnancies.
