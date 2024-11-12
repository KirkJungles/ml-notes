# Classification and Regression Trees

Decision trees can be used for both classification and regression, making them useful for tabular data.

This page will cover vanilla CARTs, Random Forests, ADABoost, and XGBoost.

## Regression Tree

Consider a tabular data matrix $$X$$ with corresponding target vector $y$.

A RegressionTree will take one or more entries of $X$ and provide an output $\hat{y}$.

Key parameters:
- criterion='squared_error' (Criteria used to determine bestness of fit)
- max_depth=None (How many nodes deep can a tree be built)
- min_samples_split=2 (How many samples are required to split an internal node)
- min_samples_leaf=1 (How many samples must be in a leaf)

### Train

Greedy optimization. 

Each node considers all the samples in the dataset provided to it, and considers each possible feature to use to split the samples into child nodes.

Might look something like this for regression in each node:


```
Dictionary<FunctionTuple, float> errorDict = new Dictionary<(column, category), float>()


foreach column feature in dataFrame.Columns:
	if (column.Type == string):
		List<string> uniqueCategories = column.Unique()
		foreach string category in uniqueCategories:
			foreach DataRow sample in dataFrame:	
				if (sample.Column == category):
					leftSamples.AddSample(sample)
				else:
					rightSamples.AddSample(sample)
	    calculate mean of both samples sets

calculate MSE of sample sets

if current_MSE < best_MSE:
    accept this split as new best and keep searching
return at the end
					```
