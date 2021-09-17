# PIPELINES
* simple way to keep your data preprocessing and modeling code organized
* bundles preprocessing and modeling steps so you can use the whole bundle as if it were a single step
## Benefits of Pipelines
* Cleaner Code
* Fewer Bugs
* Easier to Productionize
* More Options for Model Validation: (cross-validation)
## Steps to construct the full pipeline
* Step 1: Define Preprocessing Steps
  * use <i><b>ColumnTransformer</b></i> class to bundle together different preprocessing steps.   
* Step 2: Define the Model
* Step 3: Create and Evaluate the Pipeline
  *Finally, we use the <i><b>Pipeline</b></i> class to define a pipeline that bundles the preprocessing and modeling steps. There are a few important things to notice 
    * With the pipeline, <i><b>we preprocess the training data and fit the model in a single line of code.</i></b> (In contrast, without a pipeline, we have to do imputation, one-       hot encoding,and model training in separate steps. This becomes especially messy if we have to deal with both numerical and categorical variables!)
    * With the pipeline, we supply the unprocessed features in X_valid to the predict() command, and the <i><b>pipeline automatically preprocesses the features before generating              predictions.</i></b> (However, without a pipeline, we have to remember to preprocess the validation data before making predictions.)
# When should you use cross-validation?
* For small datasets, where extra computational burden isn't a big deal, you should run cross-validation.
* For larger datasets, a single validation set is sufficient. Your code will run faster, and you may have enough data that there's little need to re-use some of it for holdout.<br><br>
* There's no simple threshold for what constitutes a large vs. small dataset. But if your model takes a couple minutes or less to run, it's probably worth switching to cross-validation.
* Alternatively, you can run cross-validation and see if the scores for each experiment seem close. If each experiment yields the same results, a single validation set is probably sufficient.
* Using cross-validation yields a much better measure of model quality, with the added benefit of cleaning up our code: note that we no longer need to keep track of separate training and validation sets. So, especially for small datasets, it's a good improvement!
# Data Leakage
* Data leakage (or leakage) happens when your training data contains information about the target, but similar data will not be available when the model is used for prediction.
* leads to high performance on the training set (possibly even the validation data), but the model will perform poorly in production.
## Types of leakage
1. target leakage <br/>
2. train-test contamination.
### Target leakage
* occurs when your predictors include data that will not be available at the time you make predictions.
* People take antibiotic medicines after getting pneumonia in order to recover. The raw data shows a strong relationship between those columns, but took_antibiotic_medicine is frequently changed after the value for got_pneumonia is determined. This is target leakage.

| got_pneumonia| age | weight | male |   took_antibiotic_medicine    |
|:------------:|:---:|:------:|:----:|:-----------------------------:|
|False	        |65	  |100	    |False	| False	...                     |
|False	        |72   |130	    |True	 | False	...                     |
|True	         |58	  |100	    |False	| True	...                      |

* To prevent this type of data leakage, any variable updated (or created) after the target value is realized should be excluded.
### Train-test contamination
example: preprocessing (like fitting an imputer for missing values) before calling train_test_split()
