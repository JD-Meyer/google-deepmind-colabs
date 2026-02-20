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

**Code point**: The unique ID number for each unicode character.

**Zipf's Law**:

**Special Tokens**
- <BOS>: Beginning of Sentence
- <EOS>: End of Sentence
- <PAD>: Padding
- <UNK>: Unknkown



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





