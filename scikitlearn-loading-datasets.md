# Scikit learn datasets are dictionaries

(thanks to [Sam Zeitlin](https://github.com/szeitlin) for the hint)



I was interested in looking at the [Boston housing prices dataset](https://archive.ics.uci.edu/ml/datasets/Housing) for testing Spark, but I didn't feel like manually downloading a .data file, converting it to csv, then pulling it into Spark. It would be nice if Python had some APIs into the data.

[Scikit-learn](http://scikit-learn.org/stable/) is a machine learning library for Python. One of the many features available through its API is a number of standard machine learning data [sets](http://scikit-learn.org/stable/datasets/). 

These datasets are dictionary-like objects called [Bunches](https://pypi.python.org/pypi/bunch/1.0.1  ): 

	from sklearn.datasets import load_boston
	boston = load_boston()
	type(boston)
	<class 'sklearn.datasets.base.Bunch'> 

From the scikit-learn documentation: 

>There are three distinct kinds of dataset interfaces for different types of datasets. The simplest one is the interface for sample images, which is described below in the Sample images section.

>The dataset generation functions and the svmlight loader share a simplistic interface, returning a tuple (X, y) consisting of a n_samples * n_features numpy array X and an array of length n_samples containing the targets y.

> The toy datasets as well as the ‘real world’ datasets and the datasets fetched from mldata.org have more sophisticated structure. These functions return a dictionary-like object holding at least two items: an array of shape n_samples * n_features with key data (except for 20newsgroups) and a numpy array of length n_samples, containing the target values, with key target.


Long story short, easy way to extract these datasets, specifically the Boston one, to a csv file, is to get keys and values, as if from a dictionary. I purposely suppressed the index from exporting to csv. 


	import sklearn
	import numpy as np
	from sklearn.datasets import load_boston
	import pandas as pd

	#Load Boston data from sklearn
	boston = load_boston()
	df = pd.DataFrame(boston['data'], columns=boston['feature_names'])
	df.to_csv('out.csv',delimiter='\n',columns=df.columns, index=False)
	
There are alternatives to accessing it this way, and many of them invovle using pandas dataframes as wrappers of scikit-learn's numpy arrays. 
 	
Converting to and from pandas dataframes to numpy objects [is pretty common](http://stackoverflow.com/questions/20485592/how-to-create-sklearn-datasets-base-bunch-object-in-scikit-learn-from-you-own-da) in working with Scikit-learn. 
