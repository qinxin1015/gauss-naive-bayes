# Gauss Naive Bayes In Python



## Table of Contents
  - [Overview](#overview)
    - [Iris Data Set](#iris-data-set)
    - [Bayes Theorem](#bayes-theorem)
    - [Normal Probability Density Function](#normal-pdf)
    - [Joint Probability Density Function](#joint-pdf)
  - [Getting Started](#getting-started)
    - [Prerequisites](#prerequisites)
    - [State By Step](#step-by-step)
      - [Data](#data)
      
## Overview 
We will be using Naive Bayes and the Gaussian Distribution (Normal Distribution) to build a classifier in Python from scratch.

The Gauss Naive Bayes Classifier will run on four classic data sets:

* [iris](http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data)
* [diabetes](https://archive.ics.uci.edu/ml/machine-learning-databases/pima-indians-diabetes/pima-indians-diabetes.data)
* [redwine](http://archive.ics.ucimachine-learning-databases/wine-quality/winequality-red.csv)
* [adult](http://archive.ics.uci.edu/ml/machine-learning-databases/adult/adult.data)


Here we'll be working with just the [iris](http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data) data set.

#### Iris Data Set:

The Iris data set is a classic and is widely used when explaining classification models. 
The data set has 4 independent variables and 1 dependent variable that has 3 different classes.

The first 4 columns are the independent variables (features).                                      
The 5th column is the dependent variable (class).

1. *sepal length* (cm)
2. *sepal width* (cm) 
3. *petal length* (cm) 
4. *petal width* (cm) 
5. classes: 
    * *Iris Setosa*, 
    * *Iris Versicolour*
    * *Iris Virginica*


#### Bayes Theorem:
![Bayes](img/bayes_exp.JPG "Bayes" )

**Class Prior Probability:** 
* This is our Prior Belief

**Likelihood:**
* We are using the [Normal Distribution (Gauss)](#normal-pdf) to calculate this. Hence, the name Gauss Naive Bayes.

**Predictor Prior Probability:**
* Marginal probability of how probable the new evidence is under all possible hypothesis. Most Naive Bayes Classifiers do not calculate this. The results do not change or change very little. Though we do calculate it here.


#### Normal PDF:
![Normal Distribution](img/normal_distribution.svg "Normal Distribution" )

See [Normal Distribution (Wikipedia)](https://en.wikipedia.org/wiki/Normal_distribution) definition.

The Normal Distribution will help determine the likelihood of a *class* occuring for each feature. In other words for each column of our dataset, the Normal Distribution will calculate the likelihood of that *class* occuring. 

#### Joint PDF:
![Alt text](img/joint_pdf.svg "Optional Title")

See [Joint PDF (Wikipedia )](https://en.wikipedia.org/wiki/Joint_probability_distribution) definition.

The Joint PDF is the product of all PDFs. In our case, the product of all Normal Distribution PDFs. Multiplying all of the PDFs gives us the likelihood.


## Getting Started

### Prerequisites


Every function is created from scratch.
However, instead of having to download the data, we're using a quick api call to get the csv.

```
$ pip install requests
```

### Step by Step

#### 1. Data
- The first 4 columns represent the **features** (*sepal length*, *sepal width*, *petal length*, *petal width*)
- The last column represents the **class** for each row. (*Setosa*, *Versicolour*, *Virginica*)

| sepal length  | sepal width | petal length | petal width | class |
| :-----------: |:-----------:| :----------: | :----------:| :----:|
| 5.1 | 3.5 | 1.4 | 0.2| Iris-setosa | 
| 4.9 | 3.0 | 1.4 | 0.2| Iris-setosa |
| 7.0 | 3.2 | 4.7 | 1.4| Iris-versicolor |
| 6.3 | 2.8 | 5.1 | 1.5| Iris-virginica |
| 6.4 | 3.2 | 4.5 | 1.5| Iris-versicolor |


#### 2. Python Code

Building the Naive Bayes Classifier.

#### Skeleton

Create the skeleton. Import the necessary libraries and create the class.

```python
# -*- coding: utf-8 -*-
from collections import defaultdict
from math import pi
from math import e
import requests
import random
import csv
import re


class GaussNB:

    def __init__(self):
        pass
        
        
def main():
    print "Here we will handle class methods."
    
    
if __name__ == '__main__':
    main()
```
Execute in terminal:
```
$ python gauss_nb.py
```


###### Output:
```
Here we will execute methods from the class.
```

##### Loading the CSV
```python
class GaussNB:

    def __init__(self):
        pass
        
    def load_csv(self, data, header=False, delimiter=','):
        """
        :param data:
        :param header:
        :param delimiter:
        :return:
        Load and convert each string of data into float
        """
        lines = csv.reader(data.splitlines(), delimiter=delimiter)
        dataset = list(lines)
        if header:
            # remove header
            dataset = dataset[1:]
        for i in range(len(dataset)):
            dataset[i] = [float(x) for x in dataset[i]]
        return dataset
        
def main():
    nb = GaussNB()
    url = 'http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data'
    data = requests.get(url).content
    data = nb.load_csv(data, header=True, delimiter=',')
    print 'Loaded Data. Columns: %s | Rows: %s' % (len(data[0]), len(data))
    
    
if __name__ == '__main__':
    main()
```

###### Output:
```
Loaded Data. Columns: 5 | Rows: 150
```

#### Splitting Data
```python
def split_data(self, data, weight):
    """
    :param data: original data set
    :param weight: percentage of data used for training
    :return:
    append rows to train while removing those same rows from data
    """
    train_size = int(len(data) * weight)
    train_set = []
    for i in range(train_size):
        index = random.randrange(len(data))
        train_set.append(data[index])
        data.pop(index)
    return [train_set, data]
```

#### Train
Calculate the mu and variance of features for each target class.

#### Test
Using the the Normal Distribution, calculate the PDF for all test features of each target class using N(x; mu, variance).
Calculate the Joint PDF of each row, by multiplying pdf results together.
Choose the highest joint pdf.


### Installing

Once cloned, running the program is as simple as calling 
```bazaar
python naive_bayes.py
```


End with an example of getting some data out of the system or using it for a little demo

## Running the tests

Explain how to run the automated tests for this system

### Break down into end to end tests

Explain what these tests test and why

```
Give an example
```

### And coding style tests

Explain what these tests test and why

```
Give an example
```

## Authors

* **Oleh Dubno** - [github.odubno](http://odubno.github.io/)
* **Danny Argov**

See also the list of [contributors](https://github.com/odubno/naive_bayes/graphs/contributors) who participated in this project.


## Acknowledgments


#### Sources:
Hat tip to the authors that made this code possible: 

| Author                  | URL           |
| -------------           |:-------------:|
| Dr. Jason Brownlee      | [How To Implement Naive Bayes From Scratch in Python](https://machinelearningmastery.com/naive-bayes-classifier-scratch-python/) |
| Chris Albon             | [Naive Bayes Classifier From Scratch](https://chrisalbon.com/machine-learning/naive_bayes_classifier_from_scratch.html) |
| Sunil Ray               | [6 Easy Steps to Learn Naive Bayes Algorithm](https://www.analyticsvidhya.com/blog/2017/09/naive-bayes-explained/) |
| Rahul Saxena            | [How The Naive Bayes Classifier Works In Machine Learning](http://dataaspirant.com/2017/02/06/naive-bayes-classifier-machine-learning/) |
| Data Source             | [UCI Machine Learning](http://archive.ics.uci.edu/ml/index.php) |

#### Inspiration:  
Project for Columbia Probability and Statistics course - Prof. Banu Baydil
