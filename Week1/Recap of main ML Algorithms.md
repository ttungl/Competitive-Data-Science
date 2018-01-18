# Recap of main ML Algorithms

## Linear
	- Logistic regression
	- SVM
	* Limits:
		+ two sets of points that form rings => Linear will fail in this case.
	* Implement:
		+ SKlearn
		+ Vowpal wabbit (for really large data sets)


## Tree-based
	- Decision Tree
		+ Given two sets of points, let's separate one class from another by a line parallel to the one of the axes. We use such restrictions as it significantly reduces the number of possible lines and allows us to describe the line in a simple way. After splitted into sub spaces, upper one will have a probability of gray color = 1, and lower one has a prob of gray = 0.2. The upper space doesn't require any further splitting. Now, we consider the lower space, and it's splitted into two sub spaces, where on the left space has a prob of gray = 0, and on the right space has a prob of gray = 1. 

		+ Decision tree uses divide-and-conquer approach to recurse subspace splitted into smaller subspaces. A single decision tree can be imagined as dividing a space into boxes and approximating data with a constant inside of these boxes.

	- Famous of decision tree algorithms are Random Forests and Gradient Boosted Decision Trees.

	- Keep in mind that it's hard to capture linear dependencies since it requires a lot of splits.

	- Random Forests and GBDT ~ Gradient Boosted Decision Trees
		+ Library: SKlearn and dmlcXGBoost
	
	- Additional materials
		+ [Scikit-Learn (or sklearn) library](http://scikit-learn.org/)
		+ [Overview of k-NN (sklearn's documentation)](http://scikit-learn.org/stable/modules/neighbors.html)
		+ [Overview of Linear Models (sklearn's documentation)](http://scikit-learn.org/stable/modules/linear_model.html)
		+ [Overview of Decision Trees (sklearn's documentation)](http://scikit-learn.org/stable/modules/tree.html)
		+ [Overview of algorithms and parameters in H2O documentation](http://docs.h2o.ai/h2o/latest-stable/h2o-docs/data-science.html)

	- Additional tools

		+ [Vowpal Wabbit repository](https://github.com/JohnLangford/vowpal_wabbit)
		+ [XGBoost repository](https://github.com/dmlc/xgboost)
		+ [LightGBM repository](https://github.com/Microsoft/LightGBM)
		+ [Interactive demo of simple feed-forward Neural Net](http://playground.tensorflow.org/)
		+ Frameworks for Neural Nets: Keras,PyTorch,TensorFlow,MXNet, Lasagne
		+ [Example from sklearn with different decision surfaces](http://scikit-learn.org/stable/auto_examples/classification/plot_classifier_comparison.html)
		+ [Arbitrary order factorization machines](https://github.com/geffy/tffm)



## kNN



## Neural Networks


