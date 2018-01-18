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

		+ Don't need any assumptions of the model or linearity in the data set.

+ Gradient Boosting
		
	+ 


+ kNN

	+


## QuZzz...

