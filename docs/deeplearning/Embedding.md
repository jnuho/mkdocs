---
draft: false
date: 2024-09-04
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

SBERT is a sentence embedding model.

<!-- more -->

<p align="left"><strong>Date:</strong> Auguest 20, 2024<br></p>

Large language models (LLMs) like `mixedbread-ai/mxbai-embed-large-v1` use text embeddings to represent words and sentences as high-dimensional vectors. These embeddings are trained to capture semantic relationships, making the distance between vectors a good proxy for semantic similarity.

For example, in the context of NLP:
1. The embeddings for "machine learning" and "artificial intelligence" would be close in vector space, reflecting their related concepts.
2. Conversely, the embeddings for "machine learning" and "ancient history" would be far apart, indicating their semantic dissimilarity.

This property of text embeddings is crucial for various NLP tasks such as:
- Semantic search
- Document classification
- Question answering
- Text summarization

By leveraging these semantic relationships, LLMs can understand context, generate relevant responses, and perform complex language tasks more effectively.


<!-- <img src="https://docs.aws.amazon.com/images/sagemaker/latest/dg/images/jumpstart/jumpstart-fm-rag.jpg" target="_blank" width=550> -->

<!-- <sub><i>The following diagram shows the conceptual flow of using RAG with LLMs.: Original image credited to aws.amazon.com</i></sub> -->

<!-- more -->

