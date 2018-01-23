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

## Preprocessing

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

+ **Outliers**:






