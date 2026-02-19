# Introduction to Language Models
**Deep Learning**
- class of ML
- foundation of modern LLMs

**Language Modeling**
- Languages follow rules, like syntax and grammar
- If you can teach a machine the rules for spoken language, it can learn the rules for similar pattern-modeling systems
  - Climate modeling
  - Protein folding
  - Writing music
  - Coding

* A language model with a low temperature is deterministic.

## N-grams
**N-gram**: A continuous sequence of $n$ words.
> Unigram n=1
> Bigram  n=2
> Trigram n=3

**Context**: The preceding sequence of $n-1$ words.

**How are n-grams related to the context?** N-gram models use n-grams to estimate the probability of the next word based on the context.

**Text Corpus**: A dataset consisting of a collection of texts

N-grams are limited by
- the size of the dataset
- items omitted from dataset
- reliance on frequency
- lack of long-range dependencies

**Training**: teaching a model to perform a specific task using a dataset

**Parameters**: The outputs of a training process (not the output of the application)
- the parameters of an n-gram model are conditional probabilities
- the parameters of a xformer model are a (much larger) collection of numbers

**Greedy sampling**: The practice of always choosing the token with the highest probability.

**Stochastic**: random (usually meaning as opposed to deterministic/fixed)

**Inference**: Using a machine learning model to make predictions.

**The Training Process**
a.k.a. *Optimization*
1. Predict the target based on the input
2. Compare the prediction to the target
3. Adjust the parameters

**Loss**: The difference between the target and the actual prediction.
a.k.a wrongness
high loss=large difference
decreasing loss->model is improving

**Preprocessing**: Cleaning & prepping data for model training.

**Fine-tuning**: Adpats a model to a specific task/behavior

**SFT**: Supervised Fine-Tuning

**RLHF**: Reinforcement Learning from Human Feedback
Aligns the AI's behavior with human preferences.



