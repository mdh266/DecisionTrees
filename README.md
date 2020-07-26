[![Build Status](https://travis-ci.com/mdh266/RandomForests.svg?branch=master)](https://travis-ci.com/mdh266/RandomForests)
[![codecov](https://codecov.io/gh/mdh266/RandomForests/branch/master/graph/badge.svg)](https://codecov.io/gh/mdh266/RandomForests)


# Random Forests In Python
--------------

## Intoduction
-------------
I started this project to better understand the way [Decision trees](https://en.wikipedia.org/wiki/Decision_tree) and [random forests](https://en.wikipedia.org/wiki/Random_forest) work. At this point the classifiers are only based off the gini-index and the regression models are based off the mean square error. Both the classifiers and regression models are built to work with [Pandas](http://pandas.pydata.org) and [Scikit-Learn](https://scikit-learn.org/)

## Example
    from randomforests import RandomForestClassifier
	from sklearn.model_selection import train_test_split
	from sklearn.model_selection import GridSearchCV
    from sklearn.pipeline import Pipeline
    from sklearn.metrics import accuracy_score
    from sklearn.datasets import load_breast_cancer
	dataset = load_breast_cancer()

	cols = [dataset.data[:,i] for i in range(4)]

	X = pd.DataFrame({k:v for k,v in zip(dataset.feature_names,cols)})
	y = pd.Series(dataset.target)

	X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.25, random_state=24)

	pipe   = Pipeline([("tree", RandomForestClassifier())])

    params = {"forest__max_depth": [1,2,3]}

    grid   = GridSearchCV(pipe, params, cv=5, n_jobs=-1)
    model  = grid.fit(X,y)

    preds  = model.predict(X_test)

    print("Accuracy: ", accuracy_score(preds, y_test))

    >> Accuracy:  0.8741258741258742

## Installing
-----------------

Uses the `setup.py` generated by [PyScaffold](https://pypi.org/project/PyScaffold/).  To install the library in development mode use the following:

    python setup.py develop


## Test
-----------------
Uses the `setup.py` generated by [PyScaffold](https://pypi.org/project/PyScaffold/):

    python setup.py test

## Dependencies
--------------
Dependencies are minimal:

    - Python (>= 3.6)
    - [Scikit-Learn (>=0.23)](https://scikit-learn.org/stable/)
    - [Pandas (>=1.0)](https://pandas.pydata.org/)


## References
---------------
- [An Introduction To Statistical Learning](http://www-bcf.usc.edu/~gareth/ISL/)

- [Elements Of Statistical Learning](http://statweb.stanford.edu/~tibs/ElemStatLearn/)

- [Scikit-learn Ensemble Methods](http://scikit-learn.org/stable/auto_examples/index.html#ensemble-methods)

- [Scikit-Learn Custom Estimators](https://scikit-learn.org/dev/developers/develop.html)

- [How to Implement Random Forest From Scratch In Python](http://machinelearningmastery.com/implement-random-forest-scratch-python/)

- [How To Implement A Decision Tree From Scratch In Python](http://machinelearningmastery.com/implement-decision-tree-algorithm-scratch-python)
