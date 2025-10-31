---
title: "The distribution of t"
teaching: 7
exercises: 0
---

:::::::::::::::::::::::::::::::::::::: questions 

- What is the central limit theorem?
- What does it predict for the distribution of $t$?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Introduce the Central limit theorem.
- Explain that it gives a theoretical distribution for $t$.

::::::::::::::::::::::::::::::::::::::::::::::::


### The central limit theorem

Please watch [this 3 min video](https://www.youtube.com/watch?v=jvoxEYmQHNM) to understand what the Central limit theorem is - explained with bunnies and dragons.

### Calculate a p-value using the central limit theorem

Let me sum up what we know now:  

- We have a sample of mice weights and a weight $\mu_0$ that we compare these weights to. We want to know whether the average weight differs from $\mu_0$.  
- We calculated $t$ for this specific sample. $t$ is a scaled difference between sample mean and $\mu_0$. In case the sample mean is the same as $\mu_0$, $t$ should be close to zero.  
- Moreover, the central limit theorem tells us that, if high fat diet mice in general don't differ from $\mu_0$ in their weight, we can expect $t$ to come from a standard normal distribution.  

This means, that if we sample again and again (i.e. the experiment where 20 mice were fed with special diet and weighed, and a $t$ was calculated), we should measure a different $t$ each time, and plotting the a histogram or density of $t$s will give a Gaussian bell shape.  

### The distribution of t in practice

In theory, this would be enough to calculate a p-value, but sometimes the devil is in the details. 
The Central Limit Theorem tells us that $t$ will behave like drawn from a normal distribution "if we have enough data points". So do we have enough data points in our example to be able to use it? 
It turns out in practice that for samples that have less than ~30 data points, the CLT doesn't hold, and the values of t that we calculate from the data, don’t follow a normal distribution.

The distribution of $t$s looks perfectly normal "in the middle", but not at the *tails*: We say that the distribution has *heavy tails*, because $t$ tends to take extreme values (extremely small or extremely large) more often than we would expect from a normal distribution.  

The good news is, we can still run a test on small samples, by using the *$t$-distribution* as a null distribution for $t$. This distribution looks like the normal distribution, but with heavy tails. It has one parameter, $\nu$, which specifies the degrees of freedom. Without going into detail, $\nu$ is closely connected to the number of data points (for a one-sample t-test, $\nu=N-1$). In the figure below, you see how the t-distribution changes with the sample size:


![The t distribution for different degrees of freedom (wikipedia)](fig/Student_t_pdf.svg){width="500px" alt="Graph showing t-distribution"}


For large samples, i.e. high values of $\nu$, the heavy tails vanish and the t-distribution becomes more and more similar to a normal distribution, which is exactly what the central limit theorem tells us. 

**Summary:** We can use the t-distribution as a null distribution for $t$, without worrying about the sample size.  


### Calculating the p-value using the t-distribution

For our example, you already calculated $t=2.57$ from the data for the mice on diet.
As a reminder:

``` r
t_stat <- 2.567434
```

We can now compute the p-value using the t-distribution:

``` r
t_stat <- 2.567434
N <- 20
(1-pt(t_stat,df=N-1))*2
```

In words, we define the parameter of the t-distribution `df`, based on the number of data points. We calculate the probability of $t$ being at least $2.57$ under the t-distribution (using the function `pt`), and then we multiply the result by $2$ for making the result two-sided. 

### Conclusion

At the end of the day, we can reject the null hypothesis that the sample mean equals $\mu_0$ at a 5% significance level. We conclude that the mice fed with the special diet have a different average weight than the known average weight of mice fed with a "normal" diet.  

### Congrats... 

...the worst part is over! If you could follow until here, you understood the essence of the t-test. Everything that follows is just practical details. 

![](fig/celebrate_pngwing.com.png){width="800px" alt="picture of fireworks"}

