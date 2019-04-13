---
title: "Digital Image Processing Project"
date: 2018-01-28
tags: [data wrangling, data science, messy data]
header:
  image: "/images/perceptron/percept.png"
excerpt: "Technical Analysis, Machine Learning, Support Vector Machines"
mathjax: "true"
---
### Introduction

This research discusses the viability of image processing to uncover nonlinear visual chart patterns using state of the art machine learning techniques. The expected benefit is to mimic the way technical analysts process information.

Previous papers by Lo, Mamysky, Wang (2000), Chang and Osler (1994), Fama and Blume (1966), and Sweeney (1988) have shown the ability of technical stock price patterns to predict returns. Later studies are careful to note that predictability does not necessarily imply profitability, and focus more on nonlinear chart patterns. These are discussed as being more difficult to interpret arithmetically. Additional patterns and definitions are in Pring (1988).

Pattern rules are taken from trade journals (Chang and Osler (1994)) and from print (Lo, Mamysky, Wang (2000), Edwards and McGee (1966)).

Patterns are learned using kernel density estimation and a bandwidth selection similar to Lo, Mamysky, Wang (2000). Lo, Mamysky, Wang (2000) use Cross Validated Bandwidth to automate pattern selection.

They call for more rigorous procedures to evaluate the bandwidth objectively. We remedy that. They also call for new methods to uncover the patterns which we discuss in part two of the paper.

### Methodology1

This study compares the results of several bandwidths using a local polynomial regression of order 0 and Gaussian Kernel. Some examples inlcude AICC, CV, GCV, T, etc. These are summarized in the following literature:

- "AICC"-> "AIC modified eq 2.5 in (Hurvich and Simonoff,1998)",
- "GCV"-> "Generalized Cross Validation (Graven and Wahba,1979)",
- "AIC"-> "Akaike Info Criteria (Akaike,1973)",
- "T"-> "Rice (1984)",
- "CV"-> " Leave one out cross-validation",
- "MAXP"-> "Maxium price difference, Maroney 2018

The rules for the patterns are discussed below. These are from Edwards and Mcgee (1966) and later tested empirically by Lo, Mamysky, Wang (2000).

# Pattern Definitions:

1. Head and Shoulders:
- E1 is a maximum
- E3 > E1, E3 > E5
- E1 and E5 are within 1.5 percent of their average
- E2 and E5 are within 1.5 percent of their average,

2. Inverse Head and Shoulders:
- E1 is a minimum
- E3 < E1, E3 < E5
- E1 and E5 are within 1.5 percent of their average
- E2 and E4 are within 1.5 percent of their average.

3. Broadening Top:
- E1 is a maximum
- E1 < E3 < E5
- E2 > E4

4. Broadening Bottom:  
- E1 is a minimum
- E1 > E3 > E5
- E2 < E4

5. Triangle Top:
- E1 is a maximum
- E1 > E3 > E5
- E2 < E4

6. Triangle Bottom:
- E1 is a minimum
- E1 < E3 < E5
- E2 > E4

Additional rules are in the paper by Lo, Mamysky, and Wang (2000)


For checking the reliability of the patterns professional analyst societies are noted as obtaining a CMT designation (Certified Market Technician). Other societies include: MTA, NTAA, STA, IFTA. (Linton 2010)

# Head and Shoulders

<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/hs.png" alt="head and shoulders">

## Inverse Head and Shoulders

<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/ihs.png" alt="inverse head and shoulders">

# Broadening Top
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/btop.png" alt="broadening top">

# Double Top
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/dtop.png" alt="double top">

# Conclusion

This feeds in to part two which uses state of the art machine learning tools to uncover the patterns. This is aimed at mimicking the way a trained technician sees and processes information in stock charts.

The benefit is for both academia and industry. For academia it can help with understanding pattern statistics and confidence intervals. An added benefit is aggregating bias between output and professional analyst recommendation. For industry the benefit is program trading.

The patterns are trained in a support vector machine using digital images. The images are preprocessed for extrema by pixel values.

### Confusion Matrix
<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/cm.png" alt="confusion matrix">

The inital accuracy is 72.30% for in sample data.

Although the classifier is confused with whether a rectangle bottom is a broadening bottom, it's top three misses are in other classes. This is probably becuase there are only a few rectangle bottom observations and the rules are similar to other pattern types.

<img src="{{ site.url }}{{ site.baseurl }}/images/perceptron/cm3.png" alt="confusion matrix">


R code block:
```r
library(tidyverse)
df <- read_csv("some_file.csv")
head(df)
```
