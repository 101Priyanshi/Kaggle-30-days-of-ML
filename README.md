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
