# OFFESEL

This repository contains an implementation of the OFFESEL algorithm.

We present a lightweight unsupervised feature selection algorithm for dynamic data streams which calculates the importance score of each feature in every incoming window as a weighted average of its mean normalized value

## Abstract
Feature selection methods can significantly reduce the training times of classification algorithms while preserving nearly the same predictive accuracy. However, in dynamic data streams, the feature importance may change over time. In addition, due to the limited amount of labeled data, it is important to develop unsupervised feature selection algorithms, which can make use of both labeled and unlabelled incoming instances. In this paper, we present a light- weight unsupervised feature selection algorithm for dynamic data streams called Online Fast FEature SELection - OFFESEL, which calculates the importance score of each feature in every incoming window as a weighted average of its mean normalized value. We have evaluated OFFESEL on 15 benchmark stationary and non- stationary data streams using PerceptronMask, a popular online classifier. We have compared OFFESEL to FIRES and ABFS, state-of-the-art supervised online feature selection algorithms, and to MCFS, LS, and Max Variance, popular unsupervised feature selection algorithms, which were adapted by us to nonstationary data streams. In computation time, OFFESEL has outperformed all supervised and unsupervised feature selection algorithms, while preserving the accuracy level of the supervised FIRES algorithm, which was found significantly more accurate than ABFS in our experiment.


## Installation
To use OFFESEL, you will need to install the following packages:
```python
pip install scikit-multiflow
pip install skfeature-chappers
