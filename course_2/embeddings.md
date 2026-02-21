# Embeddings
 Token indices are mapped to multi-dimensional meaning representations.

## Token embeddings
**Token embedding**: a list of floating-point numbers that represents a token. Each token gets its own unique coordinate in a high-dimensional space.

For example, our lookup table might look something like this:

Token ID 8971 (“king”) → [0.91, 0.85, -0.12, ...]

Token ID 91024 (“queen”) → [0.89, -0.78, -0.11, ...]

Token ID 87676 (“zebra”) → [-0.54, 0.23, 0.88, ...]

### Learning embeddings
The embedding table starts as a matrix of random numbers. Through the training process, the model learns that to make better predictions, it needs to nudge these vectors around.

Tokens that appear in similar contexts (like "zebra" and "wildebeest") will be pushed closer together, while tokens with different meanings will be pushed further apart. 
The embedding table is learned just like the other parameters in the model when it is trained on a dataset.


## Desired properties of embeddings
Tokens with similar meanings should be close together


**Semantic neighborhoods**: where related concepts cluster
Neighborhood A: zebra, okapi, giraffe
Neighborhood B: car, bus, train

**Cosine similarity**: measures the angle between two vectors and gives a score between -1 and 1.
- A score of 1 means the vectors point in the exact same direction (perfectly similar).
- A score of 0 means the vectors are at a 90-degree angle (unrelated).
- A score of -1 means they point in opposite directions (opposites).

**Sparse representation**: Many dimensions are zero for a given word, e.g. the "fruitiness" of the word "internet" is zero.

**Dense embeddings**: almost every number in a word's vector is a non-zero value, and each dimension contributes a small part to its overall meaning.
- Instead of having neat, human-defined axes, the model discovers the most statistically useful directions on its own.

**Distributional hypothesis**: the meaning of a word is defined by the words that appear around it
- Summarized as: "You shall know a word by the company it keeps" 
- Words that show up in similar contexts across millions of sentences tend to have similar meanings.


## Visualizing the meaning space
**Direct plotting**: Pick two or three dimensions out of the hundreds available and create a 2D or 3D scatter plot. 
While this does not show the whole picture, it can often reveal clear clusters and patterns.

**Dimensionality reduction**: Use algorithms like PCA (principal component analysis) or t-SNE. 
These methods take a high-dimensional space and intelligently project it down to 2D or 3D 
while preserving the original neighborhood structures. There is some distortion, but it gives you a very good idea of which continents are neighbors. 

**Dot Product**: indicates the similarity of two embeddings.
- Negative dot product: when $\mathbf{u}^T \mathbf{v} < 0$, the angle between them is greater than 90 degrees. The two vectors are pointing in opposite directions and this indicates a high level of dissimilarity.
- Zero dot product: when $\mathbf{u}^T \mathbf{v} = 0$, they are orthogonal and the angle between them is 90 degrees. Usually the embeddings are unrelated.
- Positive dot product: when $\mathbf{u}^T \mathbf{v} > 0$, the angle between them is less than 90 degrees. The vectors are pointing in a similar direction, meaning the embeddings are similar.

**Cosine Similarity**:  Normalizes the similarities between two vector embeddings to make them less dependent on the specific values and the number of dimensions.

**t-SNE**: A visualization method that **preserves the pairwise similarities** between data points in a lower-dimensional space.


