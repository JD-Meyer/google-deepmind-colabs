# Subword tokenization
Automatically split texts into subword tokens using the byte pair algorithm.

### An ideal tokenizer should be smart enough to:
- Keep common words as single tokens (e.g., “the”, “market”, “Nairobi”).
- Break down rare or complex words into smaller, meaningful subword units (e.g., tokenization → “token”, “ization”).
- Handle completely unknown words by breaking them down into characters and other subword units, avoiding the out-of-vocabulary (OOV) problem.

## The BPE algorithm
The BPE algorithm is a clever way to automatically learn the most useful subword tokens directly from your text data. It starts with the smallest possible units, individual characters, and iteratively merges the most frequent adjacent pairs into new, larger tokens.

Imagine the training data contains only the following words and their frequencies:
- deserts: 5 times
- desert: 3 times
- deserted: 2 times
- tested: 6 times

### Step 1: Initialization
First, BPE splits every word into its individual characters and adds a special end-of-word symbol, “</w>”, to mark word boundaries. 
This helps the model distinguish between “er” inside a word (like in “deserts”) and at the end of a word (like in “tester”).

The "dataset," now looks like this:
- d e s e r t s </w> (5 times)
- d e s e r t </w> (3 times)
- d e s e r t e d </w> (2 times)
- t e s t e d </w> (6 times)

The initial base vocabulary contains every unique character present:
{“d”, “e”, “s”, “r”, “t”, “</w>”}


In practice the base vocabulary is usually initialized with all 256 possible byte values (the origin of the word “byte” in byte-pair encoding). 
The final tokenizer can then map any Unicode token to a combination of one to four byte tokens,
preventing it from mapping characters that do not appear in the training data to <UNK>. 
It is easier and more intuitive to work with characters than with bytes, so all activities in this course use a BPE tokenizer 
that operates on characters instead of bytes.

### Step 2: Count all adjacent pairs
Now, count every adjacent pair of tokens across the entire corpus, respecting their frequencies. 
In the sequence “t e s t </w>” the token pairs are (t, e), (e,s), (s, t), and (t, </w>). These pair counts are accumulated in a frequency table as follows:

Token Pair	Count
d e	        10
e s	        16
s e	        10
e r	        10
r t	        10
t </w>	    3

### Step 3: Merge the most frequent pair
The most frequent pair of tokens in the corpus is “e s”. This pair of tokens is merged into a single token “es”.
The new token is added to the vocabulary. The new vocabulary is {“d”, “e”, “s”, “r”, “t”, “</w>”, “es”}.  

### Step 4: Replace tokens in corpus
All occurrences of the token pair “e s” in the dataset get replaced by the new token “es”, resulting in the following updated dataset.
- d es e r t s </w> (5 times)
- d es e r t </w> (3 times)
- d es e r t e d </w> (2 times)
- t es t e d </w> (6 times)

### Step 5: Repeat Steps 2 and 3. 
The process of counting pairs and merging the most frequent one continues for a set number of steps or until it reaches the target vocabulary size.

Using the example corpus, the second count and merge steps look like this:

Token Pair	Count
d es	    10
es e	    10
e r	        10
r t	        10
t </w>	    3

Now there are multiple pairs of tokens that have the same frequency of 10. 
Choose one pair arbitraril. For example, choose the first pair “d es” and mergie it to “des”. 

This results in the following vocabulary and dataset:

{“d”, “e”, “s”, “r”, “t”, “</w>”, “es”, “des”}

- des e r t s </w>    (5 times)
- des e r t </w>      (3 times)
- des e r t e d </w>  (2 times)
- t es t e d </w>     (6 times) 

### Final result
Repeat 9 more steps.

{“d”, “e”, “s”, “r”, “t”, “</w>”, “es”, “des”, “er”, “deser”, “desert”, “ed”, “ed</w>”, “tes”, “test”, “tested</w>”, “s</w>”}

- desert s</w>  (5 times)
- desert </w>  (3 times)
- desert ed</w> (2 times)
- tested</w> (6 times)

When the model encounters a word it has seen before, like “deserts”, it can represent it with just two tokens that it understands well: [“desert”, “s</w>”].

If it sees a brand new, out-of-vocabulary word like “tests”, it can still make sense of it by tokenizing it as [“test”, “s</w>”]. 
It recognizes the familiar components “test” and the plural marker “s</w>”, giving it a much better chance of understanding the otherwise unknown word's meaning. 
If you train a BPE tokenizer on a very big dataset, this effectively solves the OOV problem, producing a model that is much more robust towards small variations
such as the difference between “test” and “tests”.

Subword tokenization resolves many issues around punctuation that come with a space tokenizer. 
For example, if “desert” and “.” are both tokens in the vocabulary, the input to the model for the two strings “desert.” 
(with a period) and “desert” (without a period) will both include the subword token “desert”, which leads to similar results. 
With a space tokenizer, these two strings would be represented as two entirely different tokens and the model would have to 
learn that they are almost identical through a lot of extra training.


## The vocabulary size trade-off
How do you choose the number of merges?

- Too few merges leaves the vocabulary size small, which is good for handling new and rare words because most tokens are close to individual characters. 
However, it also results in long token sequences (e.g., tokenization might become ['t', 'o', 'k', 'en', 'iz', 'ation']), 
which is highly inefficient and makes it harder for the model to learn the meaning of whole words. 
A BPE tokenizer with very few merges is similar to character-level tokenization.

- Too many merges create very short, efficient sequences for common words (e.g., tokenization might be mapped to a single token ID). 
However, large vocabularies increase model size and memory usage. 
It can also learn too many tokens that are only relevant for the specific training data and do not generalize well to new words 
(e.g., it might learn “parametrization” as one token, but then have to break “parameter” into many subword tokens).

### Find a balance. 
Choose a vocabulary size large enough to represent common words and meaningful parts (like “-ed”, “-ing”, “-ion”) efficiently, 
but small enough to generalize to new words and keep the model size manageable.

## The "tokenizer tax"
Why you would you want to build your own tokenizer rather than using an existing one, such as the Gemma tokenizer?

Because most pretrained models are overwhelmingly trained on English-centric text. 
Their tokenizers are highly optimized for English, but inefficient for many other languages, including African languages.

When a tokenizer trained on English text encounters a word in Yoruba, for example, it may not have relevant sub-words in its vocabulary. 
It is forced to break the word down into many small, often single-character, pieces.

Ex. 
- A generic English-centric tokenizer, which has not been optimized on Yoruba, may tokenize Oluwaseun into “Olu”, “w”, “ase”, and “un”. 
- A Yoruba tokenizer, on the other hand, will correctly split Oluwaseun into meaningful tokens “Oluwa” (God) and “seun” (thanks).

**Most commercial language model APIs charge per token.**
In the above example, using the generic tokenizer would be twice as expensive and produce a worse result.
*Researchers call this the “tokenizer tax."*

Due to design decisions of the tokenizer, users working with less resourced languages tend to pay more for using 
commercial language models and get worse results compared to users working with English.  


By training your own tokenizer on data that is relevant to your task, you can build models that are not only cheaper to run,
but also more accurate, more efficient, and more equitable for your specific context.

