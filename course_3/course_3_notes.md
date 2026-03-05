# Course Goals
1. Understand the concept of generalization and its importance in making a model perform well on unseen data.
2. Recognize the limitations of training loss as the only metric for judging model quality.
3. Explain why good performance on training data does not guarantee real-world accuracy.
4. Explain how overfitting and underfitting impact model performance.
5. Describe how generalization and train-test splits can help to overcome overfitting and underfitting.
6. Interpret loss curves and the bias-variance trade-off. 
7. Explain how they reflect model behavior during training and testing.
8. Design and evaluate multilayer perceptrons (MLPs) to solve simple classification tasks.
9. Describe the way model complexity, including layers and units, influences generalization.
10. Explain how hyperparameter tuning, such as the number of layers or hidden units, has an impact on training loss versus test performance.
11. Experiment with overfitting mitigation techniques such as regularization, dropout, early stopping, and model capacity control.
12. Describe the role of a validation dataset. 
13. Explain why hyperparameter tuning should be performed on validation data rather than test data. 
14. Summarize the role of backpropagation in the process of training a neural network. 
15. Explain gradient-based optimization using the stochastic gradient descent (SGD) algorithm. 
16. Train a neural network. 
17. Consider the anticipated benefits and risks of AI models and how these can be addressed within your local region.

## Definitions

**Generalization**: The model's ability to apply what it learned from the training data to make accurate predictions on new, unseen data.
- Indicates that the model is not performing rote memorization.

**Signal**: The intended, underlying pattern the researcher intend that the model should learn. 
- The information that generalizes to new situations.
- The signal is highly dependent on the quality of the data and the planning that goes into training.

**Noise**: Coincidental patterns or artifacts specific to the training data but not representing a general rule.

**Artificial neuron**: Fundamental component of the multi-layer perceptron.

**MLP**: multi-layer perceptron
- Used for regression and classification tasks.
- aka Neural Net (NN)

**Classification**: Predicting the most likely class (or probability distribution over classes) for a given data point. 
- In the context of language models, the most common classification task is the prediction of the next token from a prompt.

**Regression**: Predicting a number for a data point. For example, predicting the future air temperature from data such as atmospheric pressure, wind speed, and time of year.

**Capacity**: ability to learn complex patterns
- Increases linearly with layers and neurons

**Gradient Descent**: Automatically updating a model's parameters to improve performance on training data.
- The gradient is a partial derivative computed over the entire dataset.
- Very memory-intensive.

**SGD**: stochastic gradient descent. 
- Gradient descent with a randomness factor thrown in.
- Speeds up the calculation of gradient weights by acting on a small, random subset of data at each iteration

**Bias**: Error introduced by oversimplification (underfitting).
- High-bias models are too rigid and fail to capture the intended, underlying patterns in the data. They ignore the signal.
- *Bias as a term* is a variable added to weighted sum of inputs before applying the activation function.
  - Bias shifts the activation function independently of its outputs.

**Underfitting**: An underfit model performs poorly both on situations in the training data, and on new situations. 
- The model may not have been trained on sufficient amounts of data. 
- It may not have been trained for long enough.
- The model has too few parameters.
- It cannot capture certain patterns because they are too complex.

**Overfitting**: An overfit model fails to generalize.
- It picks up undesirable patterns in the noise and performs as if it is answering from rote memory rather than learning patterns.

**Variance**: The error of over-sensitivity.
- a.k.a overfitting
- High-variance models pay too much attention to the noise.
- The model performs exceptionally well in situations that are very similar as the ones in the training data but fails in new situations.

**Learning rate**: Determines step size at each iteration while weifghts are updated during optimization.

**Loss curves**: Plot the training loss and the test loss as a function of the epochs.

**Decision boundary**: Theoretical boundary separating classes in a classification problem.
- NNs learn this boundary implicitly.
- It frequently appears as lines or curves on data visualizations.

**Linearly-separable dataset**: the classes in the dataset can be separated by a straight line.

**Non-linearly-separable dataset**: the classes in the dataset can *not* be separated by a straight line.

**Weights**: numerical parameters representing the strength of connections between neurons.
- Iteratively adjusted during the learning process.

**Activation function**:  Introduces non-linearity into a neural network training.
- Enables NN to learn and model complex relationships and make sophisticated decisions from data.

    **ReLU**: (Rectified Linear Unit)
    - Outputs the input value if it's positive, and 0 otherwise.
    - Creates a kink in a decision boundary
    
    **Sigmoid**: A function that outputs values between 0 and 1. 
    - If $\mathbf{(z)}$ is less than 0, the sigmoid function outputs a value between 0 and 0.5.
    - If $\mathbf{(z)}$ is greater than 0, this function outputs a value between 0.5 and 1. 
    - Useful for the output layer of binary classification models since its output can be interpreted as the probability of one of the two classes.
    - Curves the  decision boundary 
    
    **SoftMax**: Designed for tasks with many possible classes. 
    - In language models, it produces a probability distribution over the entire vocabulary. 
    - This gives the likelihood of each possible token being the next one. 
    - In this case, the output consists of multiple neurons, one for each class. This means that instead of having only one value **z**,
    - there is a separate value $\mathbf{(z)}$ for each class indexed by $\mathbf{(i)}$.

*Multiple hidden layers lead to more complex decision boundaries because each layer is able to adjust the output of the layer before it.*

**Hyperparameters**: The settings that are configured before a model begins training
    - Number of layers 
    - Number of neurons per layer (dimensions)
    - Number of epochs

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

**Train-test split**: Dividing the data into multiple subsets used to train, measure, and test learning progress.

    - The training dataset 
      - usually 70%-80% of data points
      - used for training the model parameters
    
    The validation dataset
      - usually 10-15% of data points
      - used to tune hyperparameters (like how much dropout to apply) and to decide when to stop training the model.
    
    The test set 
      - usually 10-20% of data points
      - used only after all training is complete 


**Backpropagation**: the core algorithm that enables deep neural networks to learn from data.
- SGD updates the model, gradually improving predictions; however, it only works if there's a programmatic way to update every parameter repeatedly, because the math gets too complex.

**Forward pass**: the network takes an input and generates an output during training.
- Each neuron in each layer computes a weighted sum of the outputs (also known as activations) from the previous layer, adds a bias, and then applies a non-linear activation function

#### Problem: Noor's chatbot is producing irrelevant data related to Men's jackets.
Task: Design a plan to ensure the model generalizes better.

Solution:
1. Increase the size of thr training dataset.
2. Increase the amount of specific data regarding men's jackets.
3. Stock men's jackets made out of things other than wool.