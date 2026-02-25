# Signal and noise
Why machines sometimes learn undesirable patterns.

**Signal**: The intended, underlying pattern the model should learn. The information that generalizes to new situations.

**Noise**: Coincidental patterns or artifacts specific to the training data but not representing a general rule.

**MLP**: multilayer perceptron

**SGD**: stochastic gradient descent

**Generalization**: The model's ability to apply what it learned from the training data to make accurate predictions on new, unseen data.

**Bias**: Error introduced by oversimplification (underfitting).
High-bias models are too rigid and fail to capture the intended, underlying patterns in the data. They ignore the signal.

**Underfitting**: An underfit model performs poorly both on situations in the training data, and on new situations. 
- The model may not have been trained on sufficient amounts of data. 
- It may not have been trained for long enough.
- The model has too few parameters
- It cannot capture certain patterns because they are too complex.

**Variance**: The error of over-sensitivity
- a.k.a overfitting
- High-variance models pay too much attention to the noise
- The model performs exceptionally well in situations that are very similar as the ones in the training data but fails in new situations

**Loss curves**: Plot the training loss and the test loss as a function of the epochs.

**Artificial neuron**: fundamental component of the multi-layer perceptron

**MLP**: multi-layer perceptron
- Used for regression and classification tasks

**Classification**: Predicting the most likely class (or probability distribution over classes) for a given data point. 
- In the context of language models, the most common classification task is the prediction of the next token from a prompt.

**Decision boundary**: The line separating the classes of a dataset.

**Linearly-separable dataset**: the classes in the dataset can be separated by a straight line

**Non-linearly-separable dataset**: the classes in the dataset can not be separated by a straight line

**ReLU**: (Rectified Linear Unit)
- Outputs the input value if it's positive, and 0 otherwise.
- Creates a kink in a decision boundary

**Sigmoid**: A function that outputs values between 0 and 1. 
- If (**z**) is less than 0, the sigmoid function outputs a value between 0 and 0.5.
- If (**z**) is greater than 0, this function outputs a value between 0.5 and 1. 
- Useful for the output layer of binary classification models since its output can be interpreted as the probability of one of the two classes.
- Curves the  decision boundary 

**SoftMax**: Designed for tasks with many possible classes. 
- In language models, it produces a probability distribution over the entire vocabulary. 
- This gives the likelihood of each possible token being the next one. 
- In this case, the output consists of multiple neurons, one for each class. This means that instead of having only one value **z**,
there is a separate value **z(i)** for each class indexed by **i**.

- Multiple hidden layers lead to more complex decision boundaries because each layer is able to adjust the output of the layer before it.

**Regression**: Predicting a number for a data point. For example, predicting the future air temperature from data such as atmospheric pressure, wind speed, and time of year.

**Hyperparameters**: The settings that are configured before a model begins training
    - Number of layers 
    - Number of neurons per layer (dimensions)
    - Number of epochs

**Capacity**: ability to learn complex patterns
- Increases linearly with layers and neurons

**Weight Decay**: forces the model to learn simpler weights.
- a.k.a. **L2 Regularization**
- adds a penalty term to the model's loss function based on the size of its weights
- small weights = small parameters = less noise

**Dropout**: randomly *drops* neurons by making their output 0. (Does not actually remove neurons.)
- Forces the network to learn more robust features since it cannot depend on any single neuron always being active
- Prevents complex co-adaptations where neurons rely on specific other neurons.
- Applied ONLY during training (which makes sense).

**Checkpointing**: saving the model’s parameters at different times during training.
- taking a snapshot
- Allows model to check for previous epochs with better performance. If performance degrades, the model stops training.

**Early Stopping**: Stops training once the model’s performance on a validation dataset stops improving.
- See *Checkpointing* above.

**Patience**: The number of epochs. 
- This probably refers to the human's patience rather than the machine's.

**Validation sets**: A third dataset, analogous to the final exam.

    - The training dataset 
      - usually 70%-80% of data points
      - used for training the model parameters
    
    The validation dataset
      - usually 10-15% of data points
      - used to tune hyperparameters (like how much dropout to apply) and to decide when to stop training the model.
    
    The test set 
      - usually 10-20% of data points
      - used only after all training is complete 

**Gradient Descent**: Automatically updating a model's parameters to improve performance on training data.




## Course Goals
1. Understand the concept of generalization and its importance in making a model perform well on unseen data.
2. Recognize the limitations of training loss as the only metric for judging model quality and explain why good performance on training data does not guarantee real-world accuracy.
3. Explain how overfitting and underfitting impact model performance.
4. Describe how generalization and train-test splits can help to overcome this.
5. Interpret loss curves and the bias-variance trade-off and explain how they reflect model behavior during training and testing.
6. Design and evaluate multilayer perceptrons (MLPs) to solve simple classification tasks and describe the way model complexity, including layers and units, influences generalization.
7. Explain how hyperparameter tuning, such as the number of layers or hidden units, has an impact on training loss versus test performance.
8. Experiment with overfitting mitigation techniques such as regularization, dropout, early stopping, and model capacity control.
9. Describe the role of a validation dataset
10. Explain why hyperparameter tuning should be performed on validation data rather than test data.
11. Summarize the role of backpropagation in the process of training a neural network.
12. Explain gradient-based optimization using the stochastic gradient descent (SGD) algorithm.
13. Train a neural network.
14. Consider the anticipated benefits and risks of AI models and how these can be addressed within your local region.




#### Problem: Noor's chatbot is producing irrelevant data related to Men's jackets.
Task: Design a plan to ensure the model generalizes better.

Solution:
1. Increase the size of thr training dataset.
2. Increase the amount of specific data regarding men's jackets.
3. Stock men's jackets made out of things other than wool.


### Evaluate Model and System for safety
