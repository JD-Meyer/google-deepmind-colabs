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

* The input to deep learning models is a matrix where each row corresponds to the data for one example in the dataset.

## Training Your SLM (1_5)

### Padding a dataset
Create a matrix containing the indices of each token in the dataset.
- Each paragraph in the dataset will constitute a matrix.
- All matrices must be of same size, so <PAD> is used as a token to match length of longest paragraph.
    - Alternate methods include
        - truncating all paragraphs to length of shortest paragraph
        - selecting an arbitrary paragraph length, truncating long ones and padding short ones (most common method).

### Preparing the input and target datasets
- Input: contains the context of a sequence
- Target: contains the last token
ex. 'Table Mountain is beautiful
- Input: ["Table", "Mountain", "is"] (last token removed).
- Target: ["Mountain", "is", "beautiful"] (shifted by one token).

### Shuffle the dataset and specify the batch size
Batch: chunks of data, in this case, a few paragraphs per batch.
Shuffling ensures that a diverse group of each data lands in each batch. We don't want one batch to be all about coffee and another batch to be all about gorillas.
- The order of tokens w/in the paragraph must remain consistent.
Processing order:
1. Create the dataset (tokenize & encode)
2. Pad
3. Shuffle
4. Batch (select batch size)

- TensorFlow has libraries to shuffle & batch.

### Train the SLM
Our SLM will have around 3.5B parameters
------
> **ℹ️ Info: Parameters of a transformer model**
>
> **Parameters** are a set of numbers that guide the model to perform whatever task it was trained to do. In the case of transformer models, the parameters are less interpretable. They are often a very large collection of numbers that determine the model behavior.
>
> The parameters of a transformer model are updated after processing each batch of paragraphs. At the start of the training, the parameters are intialized with random numbers.
>Models are then usually trained by processing the data multiple times. Going through the data once is known as an **iteration** or **epoch**. During each training iteration, the parameters are updated so that they lead to better predictions of the next token.
------

### Initialize the model
Use create_model() to build a transformer model.
- max_length: Length of a paragraph, same as above.
- vocabulary_size: number of unique tokens in the dataset.
- learning_rate: How quickly to update the parameters.
    - High values are faster, but not as effective
    - Low values are more accurate, but slow

**Callback function**: Prints a sample output on a regular basis during training so loss can be measured.

## Train the Model!
- **Step**: The training process updates the model parameter after processing each batch. Processing & updating is a single step.
- **Epoch**: Processing all batches in the dataset. Run multiple epochs to improve accuracy.
- **Overfitting**: When you run too many epochs and the model starts picking up noise.

### Evaluation
- A. How good is your model at predicting the next token for a given prompt based on patterns identified in the training dataset?
- B. Is the generated text coherent, and does it make sense given the context?
- C. Is the likely next token what you expect to see when the context is changed slightly?

**Test set**: Curated collection of prompts and outputs. Allows the user to automate metrics.