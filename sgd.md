# Stochastic Gradient Descent (SGD)

**Batch gradient descent**: calculating the gradient descent based on all examples at once.
It works well for small datasets & small models; however,
It is computationally expensive, using large amounts of RAM.


**SGD**: approximates the true gradient using small, random samples of data.
- introduces slight noise
- computationally cheap on the order of $10^3$


### The training loop with mini-batches
- Uses epochs and mini-batches. 

The typical training loop consists of the following steps:
1. Shuffle the dataset at the beginning of each epoch.
- Ensures that the composition of individual mini-batches does not have a significant impact on the training process.
- Guarantees that the expected value of the gradient of each mini-batch is equal to the full gradient.

2. Divide the shuffled dataset into many equally-sized mini-batches.

3. For each mini-batch in the epoch,
- Feed the mini-batch of examples to the model.
- Compute the gradient of the loss for that batch.
- Use the gradient to update the model's weights
- Use the same updating formula that you have encountered in the previous lab: $w &larr; w &larr; \alpha\nabla w$
  - where $\alpha$ means learning rate

4. Each epoch ends when all mini-batches have been processed.

### Other optimizers
**Vanilla SGD** takes fixed-sized steps. Can be slow on gentle slopes or might overshoot the valley in steep ravines.

**Optimizers with momentum** Build up speed as they continue downhill, helping them roll through flat areas faster.

**Adam (adaptive moment estimation)** Improves upon optimizers with momentum by adapting step size based on slope. 
Takes large steps on flat slopes/ small steps on steep slopes.