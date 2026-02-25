# Gradients
Gradients minimize error when training ANNs.

**Gradient Descent**: Automatically updating a model's parameters to improve performance on training data.


## Finding the bottom of the valley
- Imagine the loss function as a hilly landscape.
- *Altitude* at a point represents loss for a set of weights.
- The gradient measures the slope at the point and drags the altitude down to the lowest possible point.

### Computing the gradient with the chain rule
The challenge is that the weights $\mathbf{w}$ affect the loss $\mathbf{L}$ through a series of steps: 
- changing $\mathbf{w}$ changes the dot product $\mathbf{z}$ 
- which changes the prediction $\mathbf{y}$, 
= which changes the loss $\mathbf{L}$.

Calculate the effect using the **Chain Rule** by multiplying the effects of each individual step. 

$$𝛅L/𝛅w   =    𝛅L/𝛅y   \cdot    𝛅y/𝛅z     \cdot  𝛅z/𝛅w$$
 
 as a product of three smaller, more manageable derivatives: 

### How the gradient is used
The formula for the gradient is used to update the parameters during training.

If the data point is from the positive class $\mathbf{(t=1)}$, the prediction should be close to 1.
( This happens when $\mathbf{w*x}$ is large. )
If the loss is high because $\mathbf{y}$ is too small, the gradient pushes $\mathbf{w}$ in the direction of $\mathbf{x}$ to lower the loss. 
This helps increase w*x the next time the model makes a prediction. 

If the example is from the negative class $\mathbf{(t=0)}$ and $\mathbf{y}$is too large, the gradient pushes $\mathbf{w}$ away from $\mathbf{x}$. 
Accordingly, w*x decreases when the model makes a new prediction for the same or a similar value of $\mathbf{x}$. 
This reduces the loss by reducing the predicted probability for the specific value of $\mathbf{z}$. 
The model slowly increases its confidence in the correct class over time by repeatedly applying weight adjustments.



