# Represent Your Language Data

## Course Objectives
- Explain the nuances and complexities of language data with regard to tokenization.
- Relate the token distribution in your dataset to Zipf’s law, describing the relationship between the frequency and the rank of a token.
- Discuss the trade-off between vocabulary size, model size and computational efficiency.   
- Explain the different types of tokenization methods (e.g. character, word, subword) and analyze their effects on vocabulary size and sequence length.
- Explain the role of special tokens (such as <BOS>, <EOS>, <PAD>, <UNK>) in model vocabulary.  
- Describe the byte-pair encoding (BPE) algorithm and apply it to a text dataset. 
- Recognize how embeddings capture the meaning of tokens.
- Visualize word embeddings and understand the relationship between embeddings for tokens with similar and unrelated meanings.
- Prepare a dataset for model training using a subword tokenizer and train a small language model on the preprocessed dataset.
- Critically evaluate the ethical dimensions of dataset creation, including issues of privacy, consent, ownership, and representation, and explain how these shape the fairness and accountability of LLMs.
- Design and document an ethical dataset using the Data Cards process, demonstrating how transparent, community-aligned data practices can support responsible AI development.

* Why do we clean data?
  * To reduce noise while retaining important information

## Glossary
**BPE**: Byte-Pair Encoding

**Code point**: The unique ID number for each Unicode character.

**Zipf's Law**: A very small number of tokens (like "the", "a", "and") are extremely common, while the vast majority are rare, often appearing only once. 
This creates a "long tail" distribution.

**log-log plot**: Solves the problem of the long tail when plotting distribution frequency.
- Plots the logarithm of the rank against the logarithm of the frequency.

**Special Tokens**
- <BOS>: Beginning of Sentence
- <EOS>: End of Sentence
- <PAD>: Padding
- <UNK>: Unknkown
- </w>: end of word

**High-resource languages**: Languages which have a large corpus of digitized text available to train LMs on.

**Low-resource languages**: Have a smaller digital footprint. Low-resource languages are generally under-represented.

**data coloniality**: The risk of digital data being extracted in a way that mirrors historical practices.

**OOV**: The out-of-vocabulary problem occurs when a model encounters a word not in its vocabulary.

**Subword tokenization**: Optimizes the balance between word-sized and character-sized tokens.

## The BPE Algorithm

1. **Initialize**: Split the dataset into individual characters. Initialize the vocabulary with the set of unique characters. Replaces spaces with `</w>`).
2. **Count**: Count how often each pair of tokens appears in the corpus.
3. **Merge**: Choose the most frequently appearing adjacent pair of tokens `(p, q)`. Add a new merged token `pq` to the vocabulary.
4. **Replace**: Replace all adjacent pairs of tokens `(p, q)` with the new token `pq` in the corpus.
5. **Repeat**: steps 2-4 until you reach the target vocabulary size.





-----
### **The `unicodedata` package**
>
> Python module to look up formal name, numeric value (if it has one), and general category.
> This category is particularly useful for cleaning texts.
------
| Category | Meaning            | Common sub-codes & examples |
|-------------|--------------------|-----------------------------|
| **L\***     | Letter             | `Lu` = uppercase (A), `Ll` = lowercase (a), `Lt` = titlecase (ǅ), `Lm` = modifier (ʰ), `Lo` = other letters (汉, ע) |
| **N\***     | Number             | `Nd` = decimal digits (0-9, ٠–٩), `No` = other numbers (½, Ⅻ) |
| **P\***     | Punctuation        | `Po` = other punctuation (!, ?), `Pd` = dash (—), `Ps`/`Pf`/`Pe` = start/final/end brackets |
| **S\***     | Symbol             | `Sm` = math (±, √), `Sc` = currency (₦, $), `Sk` = modifier (ˆ), `So` = other symbols (😊, ⭐) |
| **Z\***     | Separator          | `Zs` = space, `Zl` = line, `Zp` = paragraph |
| **C\***     | Other / Control    | `Cc` = control codes (newline, tab), `Cf` = formatting marks (zero-width joiner), `Cs` = surrogates, `Co`/`Cn` = private-use or unassigned |





