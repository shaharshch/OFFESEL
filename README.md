# OFFESEL

This repository contains an implementation of the OFFESEL algorithm.

We present a lightweight unsupervised feature selection algorithm for dynamic data streams which calculates the importance score of each feature in every incoming window as a weighted average of its mean normalized value

## Abstract
Feature selection methods can significantly reduce the training times of classification algorithms while preserving nearly the same predictive accuracy. Moreover, in dynamic data streams, the feature's importance may change over time.
In addition, due to the limited amount of available labeled data, it is important to develop unsupervised feature selection algorithms, which can make use of unlabelled incoming instances.
In this paper, we present a lightweight unsupervised feature selection algorithm for dynamic data streams called Online Fast FEature SELection - OFFESEL, which calculates the importance score of each feature in every incoming window as a weighted average of its mean normalized value.
We have evaluated OFFESEL on 17 benchmark stationary and non-stationary data streams using popular online classifiers such as PerceptronMask, VFDT, Online Boosting and Linear SVM. We have compared OFFESEL to FIRES and ABFS, state-of-the-art supervised online feature selection algorithms, and to MCFS, LS, and Max Variance, popular unsupervised feature selection algorithms, which were adapted by us to data streams. OFFESEL has outperformed all supervised and unsupervised feature selection algorithms in terms of computation time, while preserving the accuracy level of the supervised FIRES algorithm, which was found significantly more accurate than ABFS in our experiments.
Furthermore, OFFESEL also maintains the accuracy level achieved by the unsupervised Max Variance algorithm, which was notably faster than LS and MCFS in our experiments. It's important to highlight that OFFESEL surpasses in terms of computation time Max Variance.


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
## Results

This repository contains the results of experiments conducted using different classifiers and feature selection methods. The experiments compare the performance of the OFFESEL against various unsupervised and supervised feature selection methods, including online max variance, online LS, online MCFS, FIRES, and the full feature space.

### Folder Structure

- [lsvm](results/lsvm): Results for the LSVM classifier.
- [online_boosting](results/online_boosting): Results for the Online Boosting classifier.
- [perceptron](results/perceptron): Results for the Perceptron classifier.
- [vfdt](results/vfdt): Results for the VFDT classifier.
- [feature_selection_time](results/feature_selection_time.xlsx): Feature selection time comparison between OFFESEL and online max variance, online LS, online MCFS, FIRES.

### Subfolder Structure

Within each classifier folder (lsvm, online_boosting, perceptron, vfdt), you'll find three subfolders:

- **accuracy**: Contains accuracy comparison results.
- **training_time**: Contains training time (ms) comparison results.
- **computation_time**: Contains computation time (ms) comparison results.

Each subfolder contains three CSV files corresponding to OFFESEL comparisons with online max variance, online LS, online MCFS, FIRES, and the full feature space.


### Instructions

To explore the detailed results, navigate to the respective classifier and metric folders. The CSV files provide a comprehensive overview of the experiments.

