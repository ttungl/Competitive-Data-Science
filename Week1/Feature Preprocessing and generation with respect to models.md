# Feature Preprocessing and generation with respect to models

---

# Numeric features

## Main topics

1. Feature preprocessing

2. Feature generation

3. Their dependence on a model type

	+ Features: numeric, categorical, ordinal, datetime, coordinates.

	+ Missing values

## Titanic dataset

+ Feature preprocessing

	+ Improve quality of the model

		+ One-hot encoding.

+ Feature generation

	+ Gradient Boost decision trees


## Conclusion

+ Feature preprocessing is often necessary

+ Feature generation is powerful technique

+ Preprocessing and generation pipelines depend on a model type.


---

## Feature Preprocessing

+ **Scaling**: different scaling results in different result of the model quality.

	1. Rescale to the same scale (usually to [0,1])

			sklearn.preprocessing.MinMaxScaler

			X = (X - X.min()) / (X.max() - X.min())


		[code]

			scaler = MinMaxScaler()

			xtrain = scaler.fit_transform(train[['Age'],['SibSp']])
			
			pd.DataFrame(xtrain).hist(figsize=(10,4));


	2. To mean=0, std=1

			sklearn.preprocessing.StandardScaler

			X = (X - X.mean())/X.std()

	**Feature impact on non-tree based models will be similar to both.**


	3. Quiz

		In general case, if we apply preprocessing to a subset of features, this could lead to the situation that we used kNN to make predictions, and found out that different scalings of features may lead to a case where some features will have critical influence on predictions. Therefore, we should apply a chosen transformation to all numeric features.

+ **Outliers**: use some outliers to help preprocessing for the models. We can clip features values between two chosen values of lowerbound and upper bound. We can choose some percentiles from the feature, for example, 1st percentile and 99 percentile, this procedure is known in financial data as **winsorization**. 

	1. Features of data from 0 and 400, but there is a number of outliers with values around -1000.

			pd.Series(x).hist(bins=30)

	2. Now, clip the features for the model by calculating lower bound and upper bound values as features values at first and 99 percentiles.

			UPPERBOUND, LOWERBOUND = np.percentile(x, [1, 99])
			y = np.clip(x, UPPERBOUND, LOWERBOUND)
			pd = Series(y).hist(bins=30);

+ **Rank**: effective preprocessing for numeric features is the rank transformation. It sets spaces between proper assorted/classified values to be equal. **This can be better option than MinMaxScaler if we have outliers because rank transformation will move the outliers closer to other objects**.

	1. Example: if we apply a rank to the source of array, it will just change values to their indices:

			sorted array: rank([-100, 0, 1e5]) = [0,1,2]

			unsorted array: rank([1000, 1, 10]) =  [2,0,1]

	2. Linear models, kNN, and neural networks can benefit from this rank transformation if we have no time to handle outliers manually.

	3. Rank can be imported as a random data function from scipy.

			scipy.stats.rankdata

	4. **Important**: of rank transformation is, to apply to the **test data**, need to **store the creative mapping from features values to their rank values**. Alternatively, you can concatenate train and test data before applying the rank transformation.

+ **Maths**:

	1. Log transform:

			np.log(1 + x)

	2. Raising to the power < 1: Extract the data from square root.

			np.sqrt(x + 2/3)

	3. Often helps non-tree based models and especially **neural networks**. Both log transform and extract square root are useful because they drive to be values closer to the features' average values, and the values near zero are becoming more distinguishable. Despite the simplicity, one of these transformations can improve your neural network's results significantly.

+ **Notes**: It's beneficial to train a model on concatenated data frames produced by different preprocessings, or to mix the models training differently-preprocessed data.

---

## Feature generation (for numeric features)
Creating new features using knowledge about the features and the tasks. It helps us by making model training more simple and effective. Sometime, these features can be engineered using prior knowledge and logic, sometime, we have to dig into the data, create and check hypothesis, then use this inferred knowledge and intuition to derive new features.

+ **Ways to proceed**: 
	
	+ Prior knowledge: it turns out an ability to dig into the data, and derive the insights, this differentiates a **good competitor** and a **great one**.

	+ Exploratory Data Analysis (EDA)


	1. Example 1: Data of Real Estate with 2 columns, Price and Area. Squared area of 55 m^2, price $107k, price 1m^2=107k / 55 m^2. We can add more feature, like price per meter square. In this case, it's quite reasonable.

	2. Example 2: combined = (horizontal**2 + vertical**2)**0.5 

			  point <-combined-> water source 
				|		|
			vertical		|
				|		|
				-----Horizontal---

	3. Note: although Gradient Boosting DT is powerful, it still experiences some difficulties with approximation of multiplications and divisions. Adding size features explicitly can result in a more robust model with less amount of trees.

	4. If we have price of products as a feature, we **can add new feature indicating fractional part of these prices**. For example, if some product costs 2.49, the fractional part of its price is 0.49. This feature can help the model utilizing the differences in the perception of the people in terms of these prices. We also can find the similar patterns in tasks which require distinguishing between a human and a bot. For instance, if we have some kind of financial data like auctions, we could observe that the people tend to set round numbers as prices, or we are trying to find spambots on social networks, we can be sure that no human ever read messages with an exact interval of one second. 

	5. These show that creativity and data understanding are the keys to productive feature generation.

---

## Conclusion

1. Numeric feature preprocessing is different for tree and non-tree based models.

	a. Tree-based models do not depend on scaling.

	b. Non-tree based models significantly depend on scaling.

2. Most often used preprocessing are:

	a. MinMaxScaler - to [0, 1]

	b. StandardScaler - to mean==0, std==1

	c. Rank - sets spaces between sorted values to be equal

	d. np.log(1+x) and np.sqrt(1+x)

3. Feature generation is powered by:

	a. Prior knowledge

	b. Exploratory Data Analysis


---


# Categorical and ordinal features

+ Categorical features in Titanic dataset: Pclass (passenger class), Sex, Cabin, Embarked,

	+ Note: In numeric features, we know the difference between classes, however, Pclass is an ordinal feature in which we don't really know which difference is bigger or smaller other classes. As numeric features, we can sort and integrate an ordinal feature and expect to get similar performance. 

	+ For example, **driver's license type** is an ordinal feature, either A, B, C or D; **Education** is also an ordinal feature, either Kindergarden, college, school, undergraduate, bachelor, master, doctoral; **Ticket class**: 1,2,3, etc. These are sorted in increasingly complex order.

+ **label encoding**: 

	+ The simplest way to **encode** a categorical feature is to **map its unique value to different numbers**. This procedure is known as **label encoding**. This method works fine with two ways, because **tree methods** can split features and extract most of useful values in categories on its own. **Non-tree based**, on the other hand, can't use this method effectively.

	+ If we want to train linear model kNN or neural nets, we need to treat the categorical feature differently. For example, 

			Pclass		1		2		3
			target		1		**0**		1

		This is not linear, and linear model will be confused. Here we can use linear model predictions, and they are all around 0.5.

		+ We make two splits selecting in each unique value and reaching it independently. Thus, these entries could achieve much better score using these feature. 

	+ Let's take the categorical feature (Embarked feature) and apply label encoding. 

		+ We can apply encoding in the alphabetical or sorted order. A unique way to solve this feature namely S,C,Q.
		
			1. Alphabetical (sorted) 

				[S,C,Q] -> [2,1,3]

					sklearn.preprocessing.LabelEncoder

			2. Order of appearance (this can be right if sorted order is in some useful ways.)

				[S,C,Q] -> [1,2,3]

					Pandas.factorize

+ **Frequency Encoding**

	+ [S,C,Q] -> [0.5, 0.3, 0.2]

		encoding = titanic.groupby('Embarked').size()
		encoding = encoding/len(titanic)
		titanic['enc'] = titanic.Embarked.map(encoding)

	+ Frequency encoding can be helpful for non-tree based models. If it's correlated to the target value, linear model will utilize this dependency.

	+ If you have multiple categories with the same frequency, they won't be distinguisable in this new feature. We might apply categorization in order to deal with such ties.

		from scipy.stats import rankdata

+ We have also seen that linear models can struggle with label encoding:

					One-hot encoding

			Pclass		Pclass==1	Pclass==2	Pclass==3
			1		1
			2					1
			1		1
			3							1

				pandas.get_dummies

				sklearn.preprocessing.OneHotEncoder

		+ The way to adapt categorical features to non-tree based models is straight-forwarded. We need to make new column for each unique value in the future and put one in the appropriate place, every else will be zeros. This method is called, **one-hot encoding**. 

		+ For the above table, for each unique value of Pclass feature, we create new columns, this works well for linear methods such as kNN or neural nets.

		+ One-hot encoding is scaled because the minimum of this feature is zero, and max is one. 

		+ If we have few important numeric features and hundreds of binary features are used by one-hot encoding, it could become difficult for tree methods to use first one efficiently. In other words, tree methods will slow down, not always improving their results. In addition, it's easy to imply that if categorical feature has too may unique values, we will add too many new columns (features/predictors) with a few non-zero values. **To store new array efficiently**, knowing **sparse matrices** is needed. 

		+ Going with sparse matrices makes sense if number of non-zero values is far less than half of all the values. These matrices are useful when they work with categorical features or text data. Most of libraries can work with these sparse matrices directly include XGBoost, LightGBM, sklearn, and others. 

		+ After figuring out how to preprocess categorical features for tree based and non-tree based models, we can look into feature generation.

			Pclass		sex 		Pclass_sex
			3			male 			3male
			1 			female 			1female
			3 			female 			3female
			1 			female 			1female

		Pclass_sex
		1male 	1female 	2male 	2female 	3male 	3female
											1
				1
												1
				1


		




















---

# Datetime and coordinates



---

# Handling missing values





