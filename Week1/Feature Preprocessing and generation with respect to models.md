# Feature Preprocessing and generation with respect to models

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

## Feature generation
















