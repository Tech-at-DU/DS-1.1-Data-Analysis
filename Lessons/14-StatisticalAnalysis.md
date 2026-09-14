## Statistical Analysis: GMM, KDE, and Correlation

### Learning Objectives
By the end of this lesson, students will be able to:
1. Describe what a histogram is and what it approximates
2. Fit a Gaussian Mixture Model (GMM) and a Kernel Density Estimate (KDE) to a data sample
3. Compute and visualize correlation between features, both via `df.corr()` and from scratch (Pearson formula)

## What is a histogram?

A histogram is one method for estimating a density (see also [Applied Probability to DataFrame](09-AppliedProbabilitytodataframe.md)). This lesson introduces two model-based alternatives — GMM and KDE — that approximate the underlying probability density function instead of just binning and counting.


## Statistical Analysis
We have learned null hypothesis, and compared two-sample test to check whether two samples are the same or not
To add more to statistical analysis, the following topics should be covered:
1- Approximate the histogram of data with combination of Gaussian (Normal) distribution functions:
Gaussian Mixture Model (GMM)
Kernel Density Estimation (KDE)

2- Correlation among features

## Review
Write a function that computes and plot histogram of a given data
Histogram is one method for estimating density

## What is Gaussian Mixture Model (GMM)?
GMM is a probabilistic model for representing normally distributed subpopulations within an overall population

![](../Notebooks/Images/gmm_fig.png)

$p(x) = \sum_{i = 1}^{K} w_i \ \mathcal{N}(x \ | \ \mu_i,\ \sigma_i)$
$\sum_{i=1}^{K} w_i = 1$
https://brilliant.org/wiki/gaussian-mixture-model/

## Activity : Fit a GMM to a given data sample
Task:
1- Generate the concatenation of the random variables as follows:
`x_1 = np.random.normal(-5, 1, 3000)`
`x_2 = np.random.normal(2, 3, 7000)`
`x = np.concatenate((x_1, x_2))`
2- Plot the histogram of x
3- Obtain the weights, mean and variances of each Gaussian
Steps needed:  `from sklearn import mixture`
`gmm = mixture.GaussianMixture(n_components=2)`
`gmm.fit(x.reshape(-1,1))`

```Python
import numpy as np
import matplotlib.pyplot as plt
from sklearn import mixture

# Generate data samples and plot its histogram
x_1 = np.random.normal(-5, 1, 3000)
x_2 = np.random.normal(2, 3, 7000)
x = np.concatenate((x_1, x_2))
plt.hist(x, bins=20, density=1)
plt.show()

# Define a GMM model and obtain its parameters
gmm = mixture.GaussianMixture(n_components=2)
gmm.fit(x.reshape(-1,1))
print(gmm.means_)
print(gmm.covariances_)
print(gmm.weights_)
```
## The GMM has learn the probability density function of our data sample
Lets the gmm model generate sample from its model:
```Python
z = gmm.sample(10000)
plt.hist(z[0], bins=20, density=1)
plt.show()
```

### Kernel Density Estimation (KDE)
Kernel density estimation (KDE) is a non-parametric way to estimate the probability density function of a random variable. In other words the aim of KDE is to find probability density function (PDF) for a given dataset.
Approximate the pdf of dataset:
$p(x) = \frac{1}{Nh}\sum_{i = 1}^{N} \ K(\frac{x - x_i}{h})$
where $h$ is a bandwidth and $N$ is the number of data points

## Activity: Apply KDE on a given data sample
Task: Apply KDE on previous generated sample data x
Hint: use
`kde = KernelDensity(kernel='gaussian', bandwidth=0.6)`
```python
from sklearn.neighbors import KernelDensity

kde = KernelDensity(kernel='gaussian', bandwidth=0.6)
kde.fit(x.reshape(-1,1))

s = np.linspace(np.min(x), np.max(x))
log_pdf = kde.score_samples(s.reshape(-1,1))
plt.plot(s, np.exp(log_pdf))
```
```python
m = kde.sample(10000)
plt.hist(m, bins=20, density=1)
plt.show()
```
## KDE can learn handwritten digits distribution and generate new digits
http://scikit-learn.org/stable/auto_examples/neighbors/plot_digits_kde_sampling.html

## Correlation
Correlation is used to test relationships between quantitative variables. Some examples of data that have a high correlation:
1- Your caloric intake and your weight (positive — more calories, more weight)
2- The amount of time you study and your GPA (positive — more study time, higher GPA)

**Negative correlation** means the two variables move in opposite directions — as one goes up, the other tends to go down (e.g. hours spent on social media vs. hours of sleep).

Correlations are useful because we can find out what relationship variables have, we can make predictions about future behavior.

## Activity: Obtain the correlation among all features of iris dataset
1- Review the iris dataset. What are the features?
2- Eliminate two columns ['Id', 'Species']
3- Compute the correlation among all features.
Hint: Use `df.corr()`
4- Plot the correlation as a heatmap in Seaborn -> `sns.heatmap`
5- Write a function that computes the correlation (Pearson formula)
Hint: https://en.wikipedia.org/wiki/Pearson_correlation_coefficient
6- Compare your answer with `scipy.stats.pearsonr` for any given two features

```python
import pandas as pd
import numpy as np
import scipy.stats
import seaborn as sns

df = pd.read_csv('Datasets/Iris.csv')
df = df.drop(columns=['Id', 'Species'])
sns.heatmap(df.corr(), annot=True)

def pearson_corr(x, y):
    x_mean = np.mean(x)
    y_mean = np.mean(y)
    num = [(i - x_mean)*(j - y_mean) for i,j in zip(x,y)]
    den_1 = [(i - x_mean)**2 for i in x]
    den_2 = [(j - y_mean)**2 for j in y]
    correlation_x_y = np.sum(num)/np.sqrt(np.sum(den_1))/np.sqrt(np.sum(den_2))
    return correlation_x_y

print(pearson_corr(df['SepalLengthCm'], df['PetalLengthCm']))
print(scipy.stats.pearsonr(df['SepalLengthCm'], df['PetalLengthCm']))
```

## Check Your Understanding

Answers: [Solutions/StatisticalAnalysis.md](../Solutions/StatisticalAnalysis.md).

1. Pearson correlation ranges from -1 to +1. What do values near 0, near +1, and near -1 each mean?
2. What does fitting a GMM give you that a plain histogram doesn't?
3. `Pclass` is coded 1 (best) to 3 (worst). Why does it matter whether its correlation with `Survived` is positive or negative, not just how large it is?

## Topics
- Gaussian Mixture Models (GMM)
- Kernel Density Estimation (KDE)
- Correlation: `df.corr()`, heatmaps, Pearson correlation from scratch

## Resources
- [Gaussian Mixture Model (Brilliant.org)](https://brilliant.org/wiki/gaussian-mixture-model/)
- Read this blog [KDE](https://jakevdp.github.io/blog/2013/12/01/kernel-density-estimation/)
- [scikit-learn: KDE for generating handwritten digits](http://scikit-learn.org/stable/auto_examples/neighbors/plot_digits_kde_sampling.html)
- [Pearson correlation coefficient (Wikipedia)](https://en.wikipedia.org/wiki/Pearson_correlation_coefficient)
- Complete the [companion notebook](../Notebooks/14-StatisticalAnalysis.ipynb)

## Challenges

Deliverable: a notebook completing the GMM, KDE, and correlation activities above, plus the extension below.

1. Complete the GMM activity: fit a 2-component GMM to the generated `x` sample, print its means/covariances/weights, and generate new samples from it
2. Complete the KDE activity: fit and plot a KDE on the same `x` sample
3. Complete the correlation activity: heatmap of `df.corr()` on the Iris dataset, plus your own `pearson_corr()` function verified against `scipy.stats.pearsonr`
4. Extension: using the Titanic dataset, compute the correlation between `Fare` and `Survived`, and between `Pclass` and `Survived`. Which relationship is stronger, and does the sign (positive/negative) make sense given what `Pclass` measures?

## Self-Check
- [ ] My GMM has exactly 2 components (`n_components=2`), and its 2 means are roughly near -5 and 2, matching how `x` was generated
- [ ] My KDE curve visually tracks the shape of the histogram — two bumps, not one
- [ ] `pearson_corr(SepalLengthCm, PetalLengthCm)` ≈ **0.872**, and matches `scipy.stats.pearsonr` to at least 3 decimal places
- [ ] `Fare`-`Survived` correlation ≈ **0.257** (positive: higher fare, more likely to survive)
- [ ] `Pclass`-`Survived` correlation ≈ **-0.339** (negative: since `Pclass` 3 is the *worst* class, negative makes sense — worse class number, lower survival)
- [ ] I correctly identified `Pclass` as the stronger relationship (larger magnitude, 0.339 > 0.257) and explained why the negative sign is expected, not an error
- [ ] I got all 3 Check Your Understanding questions right (see [Solutions](../Solutions/StatisticalAnalysis.md))
