# Practice Quiz

## Materials

The following quizzes are aimed to check your knowledge of basic ML algorithms. Not all the information was covered in video lectures and we expect that you, as pointed in prerequisites, remember what is RF, GBDT, kNN.

If you don't know these abbreviations — you can check your Glossary (under Supplementary Materials tab).

You may find helpful these links while solving the quizz:

+ [Explanation of Random Forest](http://www.datasciencecentral.com/profiles/blogs/random-forests-explained-intuitively)
+ [Explanation/Demonstration of Gradient Boosting](http://arogozhnikov.github.io/2016/06/24/gradient_boosting_explained.html)
+ [Example of kNN](https://www.analyticsvidhya.com/blog/2014/10/introduction-k-neighbours-algorithm-clustering/)

## Review

+ Random Forests

	+ There are two keys, random and forests. 

	+ **Forest** Random forest is a collection of many decision trees. Instead of relying on a single decision tree, you build many decision trees, say 100 of them. You know what a collection of trees is called, a Forest.

	+ **Random**, say our data set has 1000 rows and 30 columns. There are two levels (row and column) of randomness in this algorithm.

		+ At row level: Each of decision trees gets a random sample of training data (say 10%), i.e. each of these trees will be trained independently on 100 randomly chosen rows out of 1000 rows of data. So the prediction results of each decision tree will be totally different from other decision trees since it's getting trained on 100 random rows from the data set.

		+ At column level: The second level of randomness is introduced. Not all the columns are passed into training each of the decision trees, i.e. only want 10% of columns sent to each tree. This means a randomly selected 3 columns will be sent to each tree, the first tree may be getting trained with C1, C2 and C4, the next decision tree may have C4, C7 and C10, so on so forth.

	+  The results from each of decision trees are taken and the final verdict will be lying on the majority voting and averaging in order to predict in case of classification and regression, respectively.

	+ **When NOT to choose Random Forests (RFs) ?** 

		+ **Random Forests don't train well on small data sets**. In this case, Linear regression will easily estimate the solution while RF will fail to do so with a good estimation.

		+ **Interpretability problem with Random Forests**. We can't see or understand the relationship between the response and the independent variables. Random Forest is a predictive tool, not a descriptive one. 

		+ **High time complexity for training in Random Forests**. It may take too long since getting trained multiple decision trees. Time complexity could increase exponentially in cases of categorical variables, i.e., a categorical column with n levels, Random Forests will split 2^n-1 points to find the max splitting point. Using H2O to train random forests to speed up the process.

		+ **Range of values** In a regression setting, the range of values is determined by the values already available in the training set, however, Random Forests cannot take values outside of the training data.

	+ **Advantages of using Random Forests**

		+ Since using multiple decision trees, **the bias** remains the same as that of a single decision tree. However, **the variance** decreases, resulting in decreasing the chance of overfitting. [Read more Bias-Variance Curse](http://manishbarnwal.com/blog/2017/02/08/the_curse_of_bias_and_variance/). 
			+ Bias is the error that captures the difference of the predicted value from the ground truth value. Bias tends to decrease when the complexity of the model increases. 

			+ When the model complexity increases, variance increases, so the chance of overfitting increases. Coming to random forests and linear regression example, random forest's variance is expected to be higher than that of linear regression model.

		+ Don't need any assumptions of the model or linearity in the data set.

+ Gradient Boosting (GB)
		
	+ **How the gradient boosting algorithm works ?**

		+ Let's revisit how a decision tree works. A decision tree is a simple **classifier which splits the space of features into regions by applying trivial splitting** (e.g. x2 < 2.4). The output regions have a rectangular form, where the predictions are constant in each region.

		+ **Gradient Boosting relies on regression trees** (even when solving a classification problem) **which minimize mean squared error (MSE)**. Selecting a prediction for a leaf region is simple: to minimize MSE, we should select an average target value over samples in the leaf. **The tree is built starting from the root: for each leaf, a split is selected to minimize MSE** for this step. This process produces suboptimal results, so building an optimal tree may turn to be a NP-Complete problem.

		+ Gradient Boosting is able to provide smooth detailed predictions by combining many trees of very limited depth.


	+ **What is gradient boosting ?**

		+ Gradient boosting is an ensembling technique, in which the prediction is done by an ensemble of simpler estimators. In practice, we use Gradient Boosting over Decision Trees (GBDT). In theory, any estimators can be used instead of decision trees.

		+ The aim of GB is to create/train an ensemble of trees. **Boosting** indicates an ensemble to work much better than a single estimator (i.e. a decision tree).

		+ How an ensemble is built ?

			+ Gradient Boosting builds an ensemble of trees **one-by-one**, then predictions of each trees are summed.

				D(x) = dt1(x) + dt2(x) + .. + dtn(x)

			+ Next decision tree tries to cover the discrepancy between the target function f(x) and current ensemble prediction by **reconstructing the residual**. For example, if an ensemble has 3 trees, the predictions of that ensemble is: D(x) = dt1(x) + dt2(x) + dt3(x). 

			+ The next tree should complement well to the existing trees and minimize the training error of the ensemble. D(x) + dt4(x) = f(x). To reconstruct the residual which is the difference between the target function and the current predictions of an ensemble. R(x) = f(x) - D(x).
			If decision tree completely reconstructs R(x), the whole ensemble gives predictions without errors.


+ kNN

	+ **When to use kNN algorithms ?**

		+ kNN can be used for both classification and regression predictive problems. kNN is commonly used in **classification problems**.

	+ **How does the kNN work ?**

		+ Choose a class that has a majority voting.

		+ What is the best K ? When K increases, the boundary becomes smoother. When k goes to infinite, the boundary becomes all one kind depending on the total majority. 

		+ Error rate at k=1 always is zero for training sample. This is because the closest point to any training point is itself, so the prediction is always accurate with k=1. Thus, k=1 resulted in overfitting the boundaries. Then, error rate decreases until reaching a minimal. After the minimal point, it then increases with the k increasing. The optimal value of k is the mininal error rate point, and can be used for all predictions.



## QuZzz...



































