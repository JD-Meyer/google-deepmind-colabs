# The multilayer perceptron (MLP)

**MLP**: multi-layer perceptron
- Used for regreaasion and classification tasks

**Classification**: Predicting the most likely class (or probability distribution over classes) for a given data point. 
- In the context of language models, the most common classification task is the prediction of the next token from a prompt.

**Regression**: Predicting a number for a data point. For example, predicting the future air temperature from data such as atmospheric pressure, wind speed, and time of year.

**Artificial neuron**: fundamental component of the multi-layer perceptron
Consists of
1. Inputs (**x**): The numerical values a neuron receives. 
- A single input can, for example, be an individual dimension of an embedding of a token. 
- A single neuron can take multiple inputs, which can be represented by a vector

2. Weights (**w**): Each individual input has a corresponding weight. 
- The weight determines how much influence that input has on the neuron's decision. 
- A large positive or negative weight means the input is very important. 
- The weights for all inputs can be represented by a vector (**w**) that consists of the weights for each input. 
- The weights (**w**) are the main parameters of the neuron that are being adjusted during training.

3. Bias (**b**): A single, extra parameter that allows the neuron to shift its output up or down, independent of the input data. 
- This extra flexibility can help the model learn the patterns in the training data.

4. Weighted sum (**z**): The neuron first calculates the weighted sum of its inputs. 
- A convenient way to compute this sum is to compute the dot product between the input vector **x** and the weight vector **w**, and then adding the bias **b**

5. Activation function (**g**): The weighted sum is then passed through an activation function to produce the neuron's final output (**y**).

    *y = g(z)*

The activation function introduces non-linearity, which is essential for the network to learn complex, real-world patterns that cannot be separated by a simple straight line. 


### Common activation Functions

**ReLU (Rectified Linear Unit)**: A simple and popular choice for the output of hidden layers. It outputs the input value if it's positive, and 0 otherwise.

**Sigmoid**: A function that outputs values between 0 and 1. 
- If (**z**) is less than 0, the sigmoid function outputs a value between 0 and 0.5.
- If (**z**) is greater than 0, this function outputs a value between 0.5 and 1. 
- Useful for the output layer of binary classification models since its output can be interpreted as the probability of one of the two classes.

**SoftMax**: Designed for tasks with many possible classes. 
- In language models, it produces a probability distribution over the entire vocabulary. 
- This gives the likelihood of each possible token being the next one. 
- In this case, the output consists of multiple neurons, one for each class. This means that instead of having only one value **z**,
there is a separate value **z(i)** for each class indexed by **i**.


