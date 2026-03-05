# Computing Attention Weights
Mathematical foundations and step-by-step process of how transformer models compute attention weights.

> Transformer models predict the next token using a SoftMax classifier whose input is the contextual embedding of the last token.
 
The contextual embedding should 
1. Capture all the relevant information in the context for predicting the next token.
2. Disambiguate tokens with multiple meanings.

The **attention mechanism** incorporates information from previous tokens that:
- Contain information that provides hints about the next token.
- Contain information about the meaning of the current token.

## Computing contextual embeddings
Attention weights are used to compute contextual embeddings. 
- Assume that you have the embeddings from the previous layer stacked in a matrix $\mathbf{X}$
 such that $\mathbf{X_2}$ corresponds to the embedding for token $\mathbf{i}$.
- Assume that you have an attention vector $\alpha_i$
 that contains the attention weights for token $\mathbf{i}$, which always sum to 1.
- That means the $\mathbf{j}$-th element of $\alpha_i$ tells you how relevant the token $\mathbf{j}$
 is for computing the contextual representation of token $\mathbf{i}$
 
In other words, how much the embedding $\mathbf{X_j}$ 
 should be weighted when computing the new contextual embedding for token $\mathbf{i}$

With $\mathbf{X}$ and $\alpha_i$ 
 in place, you can compute $\mathbf{Y_i}$ as:

$\mathbf{Y_i}= $ $\sum_j\alpha_i j {X}j$


Example: visualize computation for one token $i$

|        | $\alpha_i$ |   |      | $X$  |      |                |         | $\alpha_i{_j} {X_j}$ |          |
|--------|------------|---|------|------|------|----------------|---------|----------------------|----------|
| <BOS>  | 0.25       | x | -1.4 | 2.6  | 0.12 |                | -0.35   | 0.85                 | 0.03     |
| Jide   | 0.4        | x | 0.4  | 1.4  | 0.8  |                | 0.16    | 0.54                 | 0.32     |
| is     | 0.05       | x | 0.5  | -3.4 | 1.3  | =              | 0.025   | -0.17                | 0.055    |
| hungry | 0.13       | x | 0.1  | 0.5  | -2.8 |                | 0.013   | 0.055                | -0.364   |
| .      | 0.17       | x | -1.1 | 0.1  | -0.4 |                | -0.187  | 0.017                | -0.088   |
|        |            |   |      |      |      | $\sum$         | ------- | --------             | -------- |
|        |            |   |      |      |      | $\mathbf{Y_i}$ | -0.339  | 1.202                | -0.017   |


Note that the embeddings $\mathbf{X_j}$
 for tokens with high weights will influence $\mathbf{Y_i}$
 more. Geometrically, you can imagine all the vectors $\mathbf{X_j}$
 existing at different points in space. The new vector $\mathbf{Y_i}$
 is formed by being pulled toward all of these points simultaneously. A vector $\mathbf{X_j}$
 with a high attention weight has a very strong pull, like a powerful magnet. 
In contrast, a vector with a low weight has a very weak pull. 
The final place of the new vector $\mathbf{Y_i}$
 will be much closer to the vectors that pulled on it the hardest, 
and therefore will be more similar to the vectors with a high attention weight.


## Attention head
**Attention heads**: Components in a neural network that compute the attention weight vector 
 to compute contextual embeddings. 

**Content-based dot product self-attention**: The specific type of attention mechanism used by transformer models.

**Projection**: is a transformation through matrix multiplication that allows each token to take different roles.
- Possible roles:
  - Query
  - Key
  - Value

**Query projection $(\mathbf{q_i})$**: Represents the current token that is actively seeking information.
- You want to compute the contextual embedding on this token.
- "What other tokens in this sequence are most relevant to the meaning of token $i$?"”

**Key projection $(\mathbf{k_j})$**: Represents a token $(\mathbf{j})$ in the sequence that is offering information. 
- It acts as a label or an index for that token's content. 
- The query vector is compared against all key vectors to determine relevance.

**Value projection $(\mathbf{v_j})$**: Represents the content of a token that should be passed along if it’s deemed relevant. 
- After the model decides which words are most relevant (based on the query-key comparison), 
it retrieves the value vectors of those tokens to build a new, 
context-rich representation of the original token.

## Computing the query, key, and value vectors
The model computes the projections of the embeddings $\mathbf{X}$
 of the previous layer using matrix multiplication. $\mathbf{X_i}$
 corresponds to the embedding of token $\mathbf{i}$.
When training a language model, the model learns **three projection matrices**
for each attention head in each layer:
* Query: $\mathbf{W_q}$
* Key:  $\mathbf{W_k}$
* Value: $\mathbf{W_v}$

These perform the projections to obtain the query, key, and value vectors, respectively. 
Using these three matrices, you can compute the query, key, and value vectors as follows: 
* Query: $\mathbf{q_i} = W_q X_i$
* Key:  $\mathbf{k_j} = W_k X_j$
* Value: $\mathbf{v_j} = W_v X_j$

 ## Putting it all together
The embedding $\mathbf{Y_i}$ for the $\mathbf{i}$-th 
token of the current layer is then computed in two steps:  
1. Computation of the **attention weight vector**. 
The component of this vector is computed by taking the dot product of $\mathbf{q_i}$ and $\mathbf{k_j}$,
normalizing this dot product by the square root of the size of the vectors $\mathbf{q_i}$ and $\mathbf{k_j}$, $d_k$,
and computing the softmax across all tokens $\mathbf{j}$.

The normalization prevents the dot product from becoming very big which can lead to instabilities when training a model.

${\alpha_i}{_j} = SoftMax(q_i k_j/\sqrt{d_k})$

2.  Computation of $\mathbf{Y_i}$ as the weighted sum of values $\mathbf{v_j}$ using $\alpha$.

$\mathbf{Y_i}= $ $\sum_j\alpha_i j {X}j$

Instead of doing this for every token individually, you can also stack all vectors $q$, $k$, and $v$
into matrices such that the $i$-th row in the matrix corresponds to the $i$-th vector. 
Using the resulting matrices $Q$, $K$, and $V$,
you can then compute the output of one attention head $Y$
 for all tokens using several matrix multiplications. 
This is both convenient to implement and makes the computations run much faster on specialized hardware, such as GPUs:  

$Y = SoftMax(QK^T/\sqrt{d_k})V$


    

