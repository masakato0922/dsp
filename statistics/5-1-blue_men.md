[Think Stats Chapter 5 Exercise 1](http://greenteapress.com/thinkstats2/html/thinkstats2006.html#toc50) (blue men)

>> **Exercise 5.1** In the BRFSS (see Section 5.4), the distribution of heights is roughly normal with parameters μ = 178 cm and   = 7.7 cm for men, and μ = 163 cm and   = 7.3 cm for women.  
In order to join Blue Man Group, you have to be male between 5’10” and 6’1” (see http://bluemancasting.com). What percentage of the U.S. male population is in this range? Hint: use scipy.stats.norm.cdf.

The exercise asks to return a percentage between two values given a normal distribution given parameters mean & standard deviation.


```python
# Import Relevant Libraries
from scipy import stats

# Set Values for Parameters Mu (Mean) & Sigma (Standard Deviation)
mu, sigma = 178, 7.7
```


```python
# Create a Normal Distribution Using Scipy
normal = stats.norm(loc=mu, scale=sigma)

# Convert Heights to SI Units
lower = 177.8
upper = 185.4
```


```python
# Determine Percentage of People Below 5'-10"
per_lower = normal.cdf(lower)
print('Percentage of Peopler Shorter than 5-ft 10-in:',per_lower)

# Determine Percentage of People Below 6'-1"
per_upper = normal.cdf(upper)
print('Percentage of Peopler Shorter than 6-ft 1-in:',per_upper)

# Determine Percentage of People Between 5'-10" & 6'-1"
print('Percentage of Peopler Between 5-ft 10-in and 6-ft 1-in:',per_upper-per_lower)
```

    Percentage of Peopler Shorter than 5-ft 10-in: 0.489639027865
    Percentage of Peopler Shorter than 6-ft 1-in: 0.831733710811
    Percentage of Peopler Between 5-ft 10-in and 6-ft 1-in: 0.342094682946



```python
# An Alternative Method
# Calculate the Z-Score
z_lower = (lower-mu)/sigma
z_upper = (upper-mu)/sigma
print('People 5-ft 10-in are {} standard deviations from the mean'.format(round(z_lower,4)))
print('People 6-ft 1-in are {} standard deviations from the mean'.format(round(z_upper,4)))

# Determine Percentage of People Between 5'-10" & 6'-1"
print('Percentage of Peopler Between 5-ft 10-in and 6-ft 1-in:',stats.norm.cdf(z_upper) - stats.norm.cdf(z_lower))
```

    People 5-ft 10-in are -0.026 standard deviations from the mean
    People 6-ft 1-in are 0.961 standard deviations from the mean
    Percentage of Peopler Between 5-ft 10-in and 6-ft 1-in: 0.342094682946


The results state that in the United States, roughly 49 percent of male heights are below 5'-10" while roughly 83 percent of male heights are below 83 percent. Therefore, about 34 percent of the male population in the United States are eligible to join the Blue Man Group.
