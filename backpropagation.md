# Backpropagation
An introduction to learning parameters for multi-layer neural networks.


**Backpropagation**: the core algorithm that enables deep neural networks to learn from data.
- SGD updates the model, gradually improving predictions; however, it only works if there's a programmatic way to update every parameter repeatedly, because the math gets too complex.

**Forward pass**: the network takes an input and generates an output during training.
- Each neuron in each layer computes a weighted sum of the outputs (also known as activations) from the previous layer, adds a bias, and then applies a non-linear activation function

**Loss function**: measures the wrongness of each prediction by comparing the prediction to the correct answer (target).

**Binary cross-entropy loss**: the loss function for a binary classification task.
- The goal of training is to make the BCEL as low as possible.

**Gradient descent**: incrementally adjusts weights and bias to minimize loss.


## The full training loop using backpropagation
Putting it all together, the training process involving backpropagation unfolds as follows:

1. **Initialization**: Begin with randomly initialized weights and biases.

2. **Forward pass**: For a given input, compute the output $(y^C)$ of each layer sequentially. 
The outputs are saved for reuse when computing the errors in the backward pass.

3. **Compute loss**: Once the final activation $(y^N)$ is produced, calculate the loss using the loss function.

4. **Backward pass**:
- **Output error**: Compute the error for the final layer $(𝛅^N)$ based on the loss function.
- **Backpropagate**: The error from the output layer is used to calculate the error for the second-to-last layer $(\delta$ $^N$ $^-$ $^1)$
continue this process backward until the input layer is reached.

5. **Update parameters**: When all gradients for the weights and biases are calculated, apply a gradient descent update algorithm.
SGD is most commonly used. Calculating the gradient over the full dataset can be computationally expensive and slow, 
SGD approximates this by using a small, random mini-batch of data for each update. 
The gradient from this mini-batch is a statistically good (though slightly noisy) estimate of the true gradient, making the training process much faster.

6. **Repeat**: Repeat steps 2-5 until the model's performance is satisfactory.


