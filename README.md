# Understanding the Transformer Encoder

I find that the best way to understand this concept is to first understand what exactly the input is.

## What are the shapes of my input through the encoding layer?

### Sentence:
```plaintext
"The dog is running home"
```

### Tokenization:
| The  | dog  | is  | running  | home  |
|------|------|-----|----------|------|
| 0    | 1    | 2   | 3        | 4    |

### Assigning Arbitrary Numbers:
Each word is assigned a unique numerical representation:

| 10   | 15   | 20   | 25   | 26   |
|------|------|------|------|------|
| 0    | 1    | 2    | 3    | 4    |

**Shape:** `(1, 5)` → *(batch, num elements)*

## Embeddings
Here's where **embedding** will start coming into play → we want to store certain **attributes** of each word.

Our **embedding table** will store the specific attributes for **EACH WORD IN OUR VOCABULARY**

**Shape:** `(vocab size, num attributes)`

### Why Use Word Embeddings?
- They provide useful information about words and their usage.
- After looking up words in the embedding table, the input shape changes to:

**Shape:** `(batch, num elements, num attributes)`

## Positional Encoding
The **position embedding** function works in a similar manner. 

- The **position table** has the shape: `(length of max sequence, num attributes)`
- It assigns attributes to different positions in a sequence.

### Position Lookup and Addition
1. **LOOK UP** the position values from the table.
2. **ADD** the position values to the input.

**Final Shape (with position information included):**
```plaintext
(batch, num elements, num attributes)
```

Now, there is **position information incorporated** into the embeddings.

## Now What?
It is important to understand that, from this point onward, the goal of training is to store as much information as possible in the attributes of a specific word. In other words, the objective is to store information in the 'num attributes' of the tensor with shape (batch, num elements, num attributes).

## Multi-Head Self-Attention and Feed-Forward Network
After embeddings and positional encodings are applied, the input is processed through additional layers to capture contextual relationships between words.

### Multi-Head Self-Attention
This mechanism allows the model to focus on different parts of the input sequence simultaneously, capturing relationships between words regardless of their position.

| Layer                      | Input Shape    | Output Shape   | Functionality                                       |
|----------------------------|---------------|---------------|---------------------------------------------------|
| **Multi-Head Self-Attention** | `(1, 10, 512)` | `(1, 10, 512)` | Captures relationships between words              |
| **Feed-Forward Network**   | `(1, 10, 512)` | `(1, 10, 512)` | Applies non-linear transformations to enrich representations |

### Why These Layers?
- **Multi-Head Self-Attention** allows each word to attend to all other words in the sequence, providing richer contextual understanding.
- **Feed-Forward Network** applies transformations that enable deeper feature extraction and complex pattern learning.

Together, these components form the core of modern transformer architectures, enhancing the representation of input sequences and improving downstream tasks such as translation, summarization, and more.
