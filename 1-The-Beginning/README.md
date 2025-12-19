
# Generative AI & Transformers 

This document is designed to be:
- Logically ordered (no random jumps)
- Simple in language, even when concepts are hard
- Explained from first principles
- Filled with examples so future-you can revise without confusion

---

## 1. Artificial Intelligence (AI): The Base Layer

Artificial Intelligence is the broad goal of making machines perform tasks that normally require human intelligence.

At the most fundamental level:

AI = Data + Algorithm

- Data gives experience
- Algorithm extracts patterns from that experience

If either is missing:
- No data → nothing to learn
- No algorithm → no intelligence

AI is an umbrella term, not a single technique.

---

## 2. Machine Learning (ML)

Machine Learning is a subset of AI.

Instead of writing rules manually, we let the system learn rules from data.

Core idea:
Learn a function that maps inputs → outputs.

Example:
- Input: email text
- Output: spam or not spam

The rules are not written by humans. They are learned.

---

## 3. Classic ML (Research / Traditional ML)

### What classic ML focuses on
- Prediction or classification
- Output is usually a number or label
- Humans decide which features matter

Example:
For house price prediction, humans choose:
- number of rooms
- area
- location

The model cannot see raw reality. It only sees chosen features.

### Common algorithms
- Linear Regression
- Logistic Regression
- Decision Trees
- SVM
- KNN

### Limitations
- Heavy feature engineering
- Poor with raw text
- Cannot generate new content

---

## 4. Generative AI (GenAI)

Generative AI changes the goal completely.

Instead of predicting labels, it generates new data.

### What GenAI can generate
- Text (ChatGPT)
- Code (Copilot)
- Images (DALL·E)
- Audio / Speech

Classic ML answers:
Which class is this?

GenAI answers:
What comes next?

---

## 5. Language as a Prediction Problem

Large Language Models reduce language to one task:

Predict the next token given previous tokens.

Example:
Input:  I love programming in  
Output: Python

The model does not understand programming.
It only knows probabilities learned from data.

---

## 6. Tokens and Tokenization

Models do not read text.
They read numbers.

So text is broken into tokens.

Example:
"I love AI"  
→ ["I", " love", " AI"]  
→ [40, 2154, 843]

Important points:
- Tokens are not always words
- Rare words are split
- Tokenization is fixed before training

---

## 7. Vocabulary

Vocabulary = complete list of tokens the model knows.

- Each token has a unique ID
- Size is fixed
- Example: ~50k tokens

Tradeoff:
- Larger vocab → better coverage
- Smaller vocab → faster and cheaper

---

## 8. Vector Embeddings (Where Meaning Lives)

Token IDs themselves have no meaning.

Each token ID is mapped to a vector of numbers called an embedding.

Why vectors?
Because math can represent meaning.

### Semantic meaning
Words with similar meaning have embeddings close together.

Example:
king − man + woman ≈ queen

This is not memorization.
It is geometry in vector space.

LLMs never use dictionaries.
They use distances between vectors.

---

## 9. The Word Order Problem

Embeddings capture meaning, not order.

Example:
- Dog bites man
- Man bites dog

Same words, same embeddings, different meaning.

Without order, language breaks.

---

## 10. Positional Encoding

Transformers fix order using positional encoding.

Each token embedding is combined with position information.

Final representation:
token_embedding + positional_encoding

Now the model knows:
- which word came first
- how far words are from each other

---

## 11. Neural Networks (Quick Foundation)

A neural network:
- takes numbers
- multiplies by weights
- applies activation functions
- outputs numbers

Transformers are large neural networks with attention added.

---

## 12. Why Transformers Were Invented

Before transformers:
- RNNs and LSTMs
- Sequential processing
- Slow training
- Forget long-range context

Google needed better translation models.

In 2017:
Attention Is All You Need

Key idea:
Let every word look at every other word directly.

---

## 13. Encoder–Decoder vs GPT

### Encoder–Decoder (Original Transformer)
Used in:
- Google Translate
- Summarization

Encoder reads input.
Decoder generates output.

### GPT (Decoder-Only)
GPT removes the encoder.

Why?
Because GPT only predicts the next token.

This makes GPT:
- Autoregressive
- Simpler
- Highly scalable

---

## 14. Transformer Block Structure

Each transformer block contains:
1. Self-attention
2. Feed-forward neural network
3. Residual connections
4. Layer normalization

GPT stacks many such blocks.

---

## 15. Queries, Keys, Values (QKV)

Each token embedding is projected into:
- Query: what I am looking for
- Key: what I have
- Value: the information I provide

These projections are learned.

---

## 16. Self-Attention (With Example)

Self-attention lets each word decide which other words matter.

Example:
The animal didn’t cross the street because it was tired.

The word "it" should link to "animal", not "street".

Self-attention computes this using similarity between queries and keys.

Formula:
Attention(Q,K,V) = softmax(QKᵀ / √d) × V

Higher score → more influence.

---

## 17. Multi-Head Attention

One attention head is limited.

So transformers use multiple heads.

Each head learns a different relationship:
- grammar
- subject-object links
- long-range references

All heads are combined.

---

## 18. Feed-Forward Network

After attention:
- Each token passes through the same small neural network
- Adds non-linearity
- Improves representation

---

## 19. Full GPT Data Flow

1. Input text
2. Tokenization
3. Embeddings + positional encoding
4. Transformer blocks
5. Linear layer
6. Softmax → next-token probabilities

---

## 20. Training Phase

Training teaches one thing:
Predict the next token.

Example:
"I love programming in" → "Python"

Steps:
- Forward pass
- Compute loss (cross-entropy)
- Backpropagation
- Update weights

Done over billions of samples.

---

## 21. Inference Phase

During inference:
- No learning
- Weights frozen

The model:
predicts → samples → appends → repeats

---

## 22. Softmax and Temperature

Softmax converts scores into probabilities.

Temperature controls randomness:
- Low temperature → predictable
- High temperature → creative

Formula:
softmax(logits / T)

---

## 23. Randomness vs Creativity

- Too little randomness → boring repetition
- Too much randomness → nonsense
- Creativity is controlled randomness

---

## 24. Knowledge Cutoff

LLMs do not know real-time information.

They only know what existed in training data.

This limit is called the knowledge cutoff.

To overcome it, we use tools or retrieval systems.

---

## 25. Synthetic Data Problem

Modern AI is trained on data increasingly generated by AI itself.

Risks:
- Feedback loops
- Data quality collapse
- Loss of originality

Human-created data is becoming extremely valuable.

---

## 26. Final Mental Model

A language model is simply:

f(previous_tokens) → probability(next_token)

No understanding.
No intent.
Just probability, data, and scale.

Yet scale makes it powerful.

---
