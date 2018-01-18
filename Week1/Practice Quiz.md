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





+ Gradient Boosting
	
	+


+ kNN

	+


## QuZzz...

