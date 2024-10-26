---
draft: false
date: 2024-10-16
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

<img src="https://weaviate.io/assets/images/image7-49df8d833bd2cc21c9c829e1b65a0f23.png" target="_blank" width=250>

<sub><i>Original image credited to weaviate.io</i></sub>

<!-- more -->

## What is Binary Quantization?

It is a vector compression algorithm that reduces each dimension of a vector to a single bit (0 or 1), effectively compressing an n-dimensional vector of floating-point numbers into an n-dimensional vector of bits.

## Why use Binary Quantization?

I implemented Binary Quantization for offline feature extraction using WordLlama. WordLlama ranks documents based on their similarity to a query.

This approach offers several benefits for our use case:

1. Efficient Storage: By compressing feature vectors to binary format, we can store a large number of pre-computed features with minimal disk space usage.

2. Fast Similarity Search: Binary vectors allow for rapid similarity comparisons using bitwise operations, which is crucial for quick feature matching during extraction.

3. Reduced Memory Footprint: The compressed binary vectors consume less RAM, enabling us to work with larger feature sets on resource-constrained systems.

4. Offline Capability: Pre-computed and quantized features can be loaded quickly without requiring an internet connection or real-time computation.

Here's a brief overview of how we implemented this with WordLlama:

1. Feature Extraction:
   We use WordLlama to generate high-dimensional feature vectors for our dataset.

   ```python
   from wordllama import WordLlama

   WL = WordLlama.load()
   features = WL.embed_text("Sample text for feature extraction")
   ```

2. Binary Quantization:
   We then quantize these feature vectors to binary format.

   ```python
   def binary_quantize(vector):
       return [1 if v > 0 else 0 for v in vector]

   binary_features = binary_quantize(features)
   ```

3. Storage and Retrieval:
   The binary features are stored efficiently and can be quickly loaded for offline use.

4. Similarity Search:
   During feature extraction, we perform fast similarity searches using bitwise operations.

   ```python
   def hamming_distance(a, b):
       return sum(bit1 != bit2 for bit1, bit2 in zip(a, b))

   # Find most similar pre-computed feature
   most_similar = min(pre_computed_features, key=lambda x: hamming_distance(x, query_feature))
   ```

This approach allows us to perform efficient offline feature extraction, leveraging the power of WordLlama's language understanding while optimizing for speed and resource usage through binary quantization.


However, it's important to note that Binary Quantization comes with a trade-off. While it offers these benefits, it also results in some loss of precision compared to full floating-point representations. This method is most effective for high-dimensional vectors (typically over 1024 dimensions) where the loss of precision is often outweighed by the performance gains.
