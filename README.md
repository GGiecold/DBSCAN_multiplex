DBSCAN_multiplex
----------------
----------------

Overview
--------

A fast and memory-efficient implementation of DBSCAN (Density-Based Spatial Clustering of Applications with Noise).

It is especially suited for multiple rounds of down-sampling and clustering from a joint dataset: after an initial overhead O(N log(N)), each subsequent run of clustering will have O(N) time complexity. 

As illustrated by a doctest embedded in the present module's docstring, on a dataset of 15,000 samples and 47 features, DBSCAN_multiplex processes 50 rounds of sub-sampling and clustering in about 4 minutes, whereas Scikit-learn's implementation of DBSCAN performs the same task in more than 28 minutes. 

Such a test can be performed quite conveniently on your machine: 
simply entering ```python DBSCAN_multiplex```in your terminal will prompt a doctest to start comparing the performance of the two afore-mentioned implementations of DBSCAN. 

This 7-fold gain in performance proved critical to the statistical learning application that prompted the design of this algorithm.

Installation and Requirements
-----------------------------

DBSCAN_multiplex requires Python 2.7 along with the following packages and a few modules from the Standard Python Library:
* NumPy >= 1.9
* PyTables
* scikit-learn

Upon checking that the required dependencies are installed, you can upload DBSCAN_multiplex from the official Python Package Index (PyPI) as follows:
* open a terminal window;
* type the command: ```pip install DBSCAN_multiplex```

Usage and Example
-----------------

See the docstrings associated to each function of the DBSCAN_multiplex module for more information; in a Python interpreter console, they can be viewed by calling the built-in help system, e.g., ```help(DBSCAN_multiplex.load)```. 

The following few lines show how DBSCAN_multiplex can be used for clustering 50 randomly selected subsamples out of a common Gaussian distributed dataset. This situation arises in consensus clustering where one might want to obtain and then combine multiple vectors of cluster labels.

```
>>> import numpy as np
>>> import DBSCAN_multiplex as DB

>>> data = np.random.randn(15000, 7)
>>> N_iterations = 50
>>> N_sub = 9 * data.shape[0] / 10
>>> subsamples_matrix = np.zeros((N_iterations, N_sub), dtype = int)
>>> for i in xrange(N_iterations): subsamples_matrix[i] = np.random.choice(data.shape[0], N_sub, replace = False)
>>> eps, labels_matrix = DB.DBSCAN(data, minPts = 3, subsamples_matrix = subsamples_matrix, verbose = True)
```



