---
draft: false
date: 2024-09-06
categories:
  - LLM
authors:
  - junho
---

Feature extraction is the process of extracting information from a text. It is a crucial step in many applications, such as information retrieval, question answering, and natural language processing.

<!-- more -->

## CountVectorizer

https://scikit-learn.org/stable/modules/feature_extraction.html#text-feature-extraction

CountVectorizer is a sklearn feature extraction method. It is used to convert a collection of raw documents to a matrix of token counts. It creates a bag-of-words representation of the text corpus, where each document is represented as a vector of term frequencies.

```python
from sklearn.feature_extraction.text import CountVectorizer

corpus = [
    'This is the first document.',
    'This document is the second document.',
    'And this is the third one.',
    'Is this the first document?',
]

vectorizer = CountVectorizer()
X = vectorizer.fit_transform(corpus)
print(vectorizer.get_feature_names_out())
print(X.toarray())
```

## TF-IDF

## Word Embeddings

- Word2Vec
- GloVe

## Bag of Words

- Bag of N-Grams
- Hashing Vectorizer
- Latent Dirichlet Allocation (LDA)
- Non-negative Matrix Factorization (NMF)
- Principal Component Analysis (PCA)
- Part of Speech (POS) Tagging

