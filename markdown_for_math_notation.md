
## Summation
$(\sum _{i=1}^{n}c=cn) and (\sum _{i=1}^{n}i=\frac{n(n+1)}{2})$

## Probability
Given $\mbox{A}$ is the context

Given $\mbox{B}$ is the next word

Compute the probability $P(\mbox{B} \mid \mbox{A})$:

$$P(\mbox{B} \mid \mbox{A}) = \frac{\mbox{Count}(\mbox{A B})}{\mbox{Count}(\mbox{A})}$$

## Matrix notation

$$\mathbf{a} = \begin{pmatrix} 7 \\ 3 \\ 1 \\ 4  \end{pmatrix} \ \ \  \ \ \ \ \mathbf{b} = \begin{pmatrix} 1.5 \\ -2.5 \end{pmatrix} \ \ \ \ \ \ \mathbf{c} = \begin{pmatrix} 4 \\ 4 \\ 4 \end{pmatrix}$$

$$P = \begin{pmatrix} 7 & 4\\ 3 & 5 \\ 1 & 6 \\ 4 & 7  \end{pmatrix} \ \ \  \ \ \ \ Q = \begin{pmatrix} 7 & 3 & 1 & 4 \\ 4 & 5 & 6 & 7 \end{pmatrix} \ \ \ \ \ \ R = \begin{pmatrix} 4 & 4 & 4 \end{pmatrix}$$

## Dot Product
The dot product between $K$-dimensional vectors $\mathbf{u} \in \mathbb{R}^K$ and $\mathbf{v} \in \mathbb{R}^K$ is defined as:

$$
\mathbf{u} \cdot \mathbf{v} = \sum_{k=1}^K u_k v_k
\;=\;
u_1 v_1 + u_2 v_2 + \cdots + u_K v_K $$



## Cosine similarity

$$
\text{cosine}\ \bigl(\mathbf{u},\mathbf{v}\bigr)
\;=\;
\frac{\mathbf{u}\,\cdot\,\mathbf{v}}
     {\lVert \mathbf{u} \rVert \,\lVert \mathbf{v} \rVert}
$$

where $\mathbf{u}\cdot\mathbf{v}$ is the dot product of the two vectors, and ${\lVert \mathbf{u} \rVert \,\lVert \mathbf{v} \rVert}$
are the magnitudes (lengths) of the vectors $\mathbf{u}$ and $\mathbf{v}$, respectively.

## Using \mbox
The full n-gram counts, $\mbox{ Count}(\mbox{A B})$, and the context n-gram counts, $\mbox{ Count}(\mbox{A})$, 
can be computed by counting n-grams in a dataset (**text corpus**).








