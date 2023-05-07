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
```

## Usage
1. Define the experiments: a dictionary with the names of the feature selection model and classifier (Percptron/Hoeffding Tree) to be used.
```python
expirements = {'OFFESEL' : ['percptron', 'offesel']}
```
2. Define the datasets to be used: a dictionary with the dataset name, dataset path, target index, and the number of epochs for training.
```python
datasets_info = {dataset_name :[dataset_path, target_index , 1]}
```
3. Define the filename of the CSV results file, and the headers to be used.
```python
filename = 'results.csv'
headers = ['Timestamp', 'Dataset Name', 'Model Name', 'Classifier', 'Accuracy','Computation Time', 'Feature Selection Time', 'Training Time']
```
Loop through each dataset and experiment combination, and run the apply_experiment function on each. 
This function takes in the dataset path, dataset name, target index, number of epochs, batch sizes, fractions of features, classifier, and feature selection model. 
It returns a summary dictionary with the results of the experiment.
```python
for dataset_name, dataset_params in datasets_info.items():
    for exp, exp_params in expirements.items():
        summary = apply_experiment(dataset_path=dataset_params[0], 
                                   dataset_name=dataset_name, 
                                   tgt_index=dataset_params[1], 
                                   epochs=dataset_params[2], 
                                   batch_sizes=[25, 50, 75, 100], 
                                   fractions=[0.1, 0.15, 0.2],
                                   classifier=exp_params[0], 
                                   model=exp_params[1])
```                                                                  
4. Print the summary of each experiment and write it to the CSV results file.
```python
result_string = f"{summary['Timestamp']} - Dataset: {summary['Dataset Name']}, Model: {summary['Model Name']}, Accuracy: {summary['Accuracy']}, Computation Time: {summary['Computation Time']}, Feature Selection Time: {summary['Feature Selection Time']}, Training Time: {summary['Training Time']}"

print(result_string)

with open(filename, 'a', encoding='UTF8', newline='') as file:
    dictwriter_object = DictWriter(file, fieldnames=headers)
    dictwriter_object.writerow(summary)

file.close()
```

