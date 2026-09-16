# WordPiece Tokenization

## Project Overview

This project implements the **WordPiece Tokenization algorithm from scratch using Python**.

WordPiece is a **subword tokenization algorithm** used by BERT-family models. It divides words into smaller subword tokens and uses a scoring method to select the best pair for merging.

This project demonstrates the complete WordPiece process, starting from individual characters and building a vocabulary through token merging.

## Objectives

The main objectives of this project are:

* Understand the basic concept of WordPiece Tokenization
* Create an initial vocabulary from characters
* Calculate token frequencies
* Calculate pair frequencies
* Calculate WordPiece scores
* Find the highest-scoring pair
* Merge tokens and update the vocabulary
* Tokenize a new word using the learned vocabulary
* Convert tokens into token IDs
* Handle unknown words using `[UNK]`

## Technologies Used

* Python
* JupyterLab
* Collections module

## Project Structure

```text
WordPiece-Tokenization/
│
├── WordPiece_Tokenization.ipynb
└── README.md
```

## Training Data

The project uses a simple training dataset:

```python
words = {
    "hug": 2,
    "hugs": 1,
    "pug": 1
}
```

The frequency represents how many times each word occurs in the training data.

For example:

* `hug` occurs 2 times
* `hugs` occurs 1 time
* `pug` occurs 1 time

## Initial Tokenization

The words are initially split into individual characters.

```text
hug  -> h ##u ##g
hugs -> h ##u ##g ##s
pug  -> p ##u ##g
```

The `##` symbol indicates that the token occurs inside a word and is not the first character of the word.

## Initial Vocabulary

The initial vocabulary contains the individual character tokens:

```python
vocab = [
    "h",
    "p",
    "##u",
    "##g",
    "##s"
]
```

## Token Frequencies

The frequency of each token is calculated from the training data.

Token frequency helps determine how frequently individual tokens occur in the dataset.

The project calculates these frequencies using Python's `collections` module.

## Pair Frequencies

After calculating token frequencies, the project identifies pairs of adjacent tokens.

For example:

```text
h + ##u
##u + ##g
##g + ##s
```

The frequency of each pair is calculated based on the word frequencies in the training dataset.

## WordPiece Scoring

WordPiece does not simply select the most frequent pair.

Instead, it calculates a score using the frequency of the pair and the frequencies of the individual tokens.

The scoring formula used in this project is:

```text
Score = Pair Frequency / (Frequency of First Token × Frequency of Second Token)
```

The pair with the highest score is selected for merging.

## Finding the Best Pair

The project compares the scores of all available token pairs.

The pair with the highest WordPiece score is selected as the **best pair**.

For example:

```text
Best Pair:
##g + ##s
```

The selected pair is then merged to create a new token.

## Token Merging

After calculating the scores, the highest-scoring pair is selected for merging.

For example:

```text
##g + ##s
```

can be merged into:

```text
##gs
```

The vocabulary is then updated with the newly created token.

This process is repeated to gradually build a larger subword vocabulary.

## Vocabulary Update

After merging a pair, the newly created token is added to the vocabulary.

For example:

```text
Initial Vocabulary:
h
p
##u
##g
##s
```

After merging:

```text
##g + ##s -> ##gs
```

The vocabulary becomes:

```text
h
p
##u
##g
##s
##gs
```

The process continues until the required vocabulary size or stopping condition is reached.

## Tokenization of a New Word

After training, a new word can be tokenized using the learned vocabulary.

For example:

```text
Input:
hugs
```

The learned vocabulary may contain:

```text
hug
##s
```

Therefore, the word can be tokenized as:

```text
["hug", "##s"]
```

WordPiece searches for the **longest available subword** from the beginning of the word.

## Longest-Match Tokenization

During tokenization, the algorithm tries to find the longest matching subword.

For example:

```text
hugs
```

The tokenizer first checks whether a larger subword such as:

```text
hug
```

is available.

If it is available, the tokenizer selects:

```text
hug
```

The remaining part is:

```text
s
```

Since `s` occurs inside the word, it is represented as:

```text
##s
```

Final result:

```text
["hug", "##s"]
```

## Token IDs

After tokenization, each token can be converted into a numerical ID.

For example:

```text
Tokens:
["hug", "##s"]
```

The corresponding token IDs may be:

```text
[7, 5]
```

The exact token IDs depend on the final vocabulary and the ID assignment used by the implementation.

## Unknown Token

If WordPiece cannot completely tokenize a word using the available vocabulary, it returns:

```text
["[UNK]"]
```

`[UNK]` means **Unknown Token**.

For example:

```text
Input:
bum
```

If the tokenizer cannot represent the complete word using the learned vocabulary, the output is:

```text
["[UNK]"]
```

This prevents the tokenizer from producing incomplete or invalid token sequences.

## Complete Workflow

The complete WordPiece Tokenization workflow is:

```text
Training Data
      |
      v
Split Words into Characters
      |
      v
Create Initial Vocabulary
      |
      v
Calculate Token Frequencies
      |
      v
Calculate Pair Frequencies
      |
      v
Calculate WordPiece Scores
      |
      v
Find Highest-Scoring Pair
      |
      v
Merge the Pair
      |
      v
Add New Token to Vocabulary
      |
      v
Repeat the Process
      |
      v
Tokenize New Word
      |
      v
Convert Tokens to Token IDs
      |
      v
Handle Unknown Words using [UNK]
```

## Example

### Input Word

```text
hugs
```

### Tokenization

```text
Tokens:
['hug', '##s']
```

### Token IDs

```text
Token IDs:
[7, 5]
```

## Example Output

A sample output from the project is:

```text
Input Word: hugs

Tokens: ['hug', '##s']

Token IDs: [7, 5]
```

The notebook also displays the intermediate steps involved in the WordPiece algorithm.

## Notebook Output

The JupyterLab notebook displays:

* Token frequencies
* Pair frequencies
* WordPiece scores
* Highest-scoring pair
* Merged tokens
* Updated vocabulary
* Final vocabulary
* Tokenized words
* Token IDs
* `[UNK]` for unknown words

## How to Run

### Step 1: Install Python

Install Python on your system.

Make sure Python is added to the system PATH.

### Step 2: Install JupyterLab

Install JupyterLab using pip:

```bash
pip install jupyterlab
```

### Step 3: Open JupyterLab

Open a terminal or command prompt and run:

```bash
jupyter lab
```

### Step 4: Open the Notebook

Open the following notebook:

```text
WordPiece_Tokenization.ipynb
```

### Step 5: Run the Cells

Run each cell in order using:

```text
Shift + Enter
```

### Step 6: View the Output

The notebook displays the complete WordPiece tokenization process, including:

```text
Token Frequencies
Pair Frequencies
WordPiece Scores
Best Pair
Merged Tokens
Final Vocabulary
Tokenized Words
Token IDs
[UNK] for Unknown Words
```

## Key Concepts Demonstrated

This project demonstrates the following important concepts:

### 1. Subword Tokenization

Words can be divided into smaller meaningful pieces instead of treating every complete word as a separate token.

### 2. Vocabulary Building

The vocabulary starts with character-level tokens and grows through token merging.

### 3. Frequency Calculation

The algorithm calculates the frequency of individual tokens and token pairs.

### 4. WordPiece Scoring

The scoring formula is used to identify which pair should be merged.

### 5. Token Merging

The highest-scoring pair is merged to create a new subword token.

### 6. Longest-Match Tokenization

A new word is tokenized by finding the longest available subword tokens.

### 7. Token IDs

Tokens are converted into numerical IDs so that they can be processed by machine learning models.

### 8. Unknown Words

Words that cannot be completely represented by the vocabulary are replaced with `[UNK]`.

## Advantages

* Helps understand how subword tokenization works
* Reduces the need for a very large word-level vocabulary
* Can handle words that were not directly present in the training data
* Helps represent rare and unseen words using smaller subwords
* Provides a basic understanding of tokenization used in NLP models

## Applications

WordPiece tokenization is commonly associated with NLP systems and BERT-family models.

It can be used as part of the preprocessing pipeline for:

* Natural Language Processing
* Text Classification
* Sentiment Analysis
* Question Answering
* Text Understanding
* Language Models
* Transformer-based models

## Conclusion

This project provides a basic implementation of **WordPiece Tokenization from scratch using Python**.

It demonstrates how tokens are initialized, token and pair frequencies are calculated, WordPiece scores are computed, the highest-scoring pairs are merged, and the vocabulary is updated.

The project also demonstrates how a new word can be tokenized using the learned vocabulary, converted into token IDs, and handled as `[UNK]` when complete tokenization is not possible.

Overall, this project helps in understanding the fundamental working process of **subword tokenization and WordPiece Tokenization** used in modern Natural Language Processing systems.
