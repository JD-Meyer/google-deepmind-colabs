# Training and test splits
 Splitting data into training test sets reveals overfitting and underfitting

Datasets
1. **The training dataset**: The largest part of the data (often 80-90%), from which the model actively learns.
Analogous to homework problems. 
The model's parameters are adjusted based on the patterns that are present in this dataset.

2. The test set: This is a smaller, held-out portion of the data (the remaining 10-20%). 
The model never uses this data to train. 
It is never used to adjust the model parameters to learn patterns in this dataset.
Analogoous to exam problems.
Assesses how well the model generalizes to unseen examples.

### Loss curves 
plot the training loss and the test loss as a function of the epochs

**Underfitting (high bias)**: Training loss and test loss are high and do not decrease much, or keep decreasing until the end.
Fix by
- increasing the number of parameters, 
- Using a more sophisticated model (both of these cases will be covered in later sections of this course)
- Train the model for longer.

**Overfitting (high variance)**: The training loss consistently decreases. However, at some point, the test loss stops decreasing and starts to increase. 
- Ihe model initially learns the useful signal, so both losses decrease. 
- Later, the model starts learning patterns that are specific only to the training data (noise). 
- This makes it perform even better on the training set, hence the falling training loss, but it hurts its ability to generalize. 
- This causes it to perform worse on the unseen test data, hence the rising test loss. 
- The growing gap between the curves is the tell-tale sign of overfitting. 
Fix
- Stop training earlier at the point at which the two curves start to deviate. 
- Reduce the number of parameters of the model.

**Ideal fit**: Training loss and test loss decrease together, then level off at a low value. 
- The model is learning general patterns (the signal), from the training data that also apply to the unseen test data. 
- It is generalizing well. 
