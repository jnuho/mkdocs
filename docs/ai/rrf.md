---
draft: false
date: 2024-08-28
categories:
  - Deep Learning
  - LLM
  - Ranking
authors:
  - junho
---

<img src="https://docs.aws.amazon.com/images/sagemaker/latest/dg/images/jumpstart/jumpstart-fm-rag.jpg" target="_blank" width=550>

<sub><i>The following diagram shows the conceptual flow of using RAG with LLMs.: Original image credited to aws.amazon.com</i></sub>

<!-- more -->

<p align="left"><strong>Date:</strong> Auguest 20, 2024<br></p>

## Reciprocal Rank Fusion (RRF)

A research [paper](https://plg.uwaterloo.ca/~gvcormac/cormacksigir09-rrf.pdf) introduces the Reciprocal Rank Fusion (RRF) method for combining multiple search results (rankings).

It demonstrates that RRF outperforms both individual ranking methods and traditional ranking technique, such as the Condorcet fusion. The method is simple to implement, requires no training data, and has shown robust performance across various datasets.


- Various Retrieval Method
    - Reciprocal Rank Fusion (RRF)
    - Dense Retrieval with Transformers
    - BM25

Reciprocal Rank Fusion is a rank aggregation method that combines rankings from multiple sources into a single, unified ranking. In the context of RAG, these sources typically use different retrieval models or approaches.

The core of RRF is captured in its formula:

$$RRF(d \in D) = \sum_{r \in R} \frac{1}{k + r(d)}$$

- D is a set of documents to be ranked
- d is a document in the document set, D
- R is the set of rankers (retrievers)
- k is a constant (typically 60)
- r(d) is the rank of document d in ranker r

1.  User Query: The process begins when a user inputs a question or query.
2.  Multiple Retrievers: The query is sent to multiple retrievers. These could be different retrieval models (e.g., dense, sparse, hybrid).
3.  Individual Rankings: Each retriever produces its own ranking of relevant documents.
4.  RRF Fusion: The rankings from all retrievers are combined using the RRF formula.
5.  Final Ranking: A unified ranking is produced based on the RRF scores.
6.  Generation: The generative model uses the top-ranked documents to produce the final answer.

"Our intuition in choosing this formula derived from fact that while highlyranked documents are more important, the importance of lower-ranked documents does not vanish as it would were, say, an exponential function used."

## Text Embedding

In the context of language models, text embedding is a technique where words, sentences, or even entire documents are transformed into high-dimensional vectors. These vectors capture semantic information about the text, enabling the model to understand and process language more effectively and allowing for more effective search and retrieval.

In an information retrieval system, text embedding is used to match a user's query with the most relevant entries in the database. By comparing vector representations, the system can identify which documents are most semantically similar to the query, even if the exact words used in the query do not appear in the documents.


## Vector Database in RAG

A text embedding model (like those provided by BERT, GPT, or other transformer-based models) converts text into high-dimensional vectors (numerical representations). These embeddings capture the semantic meaning of the text in a form that can be processed mathematically.

Vector databases are specialized for storing and managing these high-dimensional vectors. They are designed to efficiently perform similarity searches and nearest-neighbor searches, which are essential for applications involving embeddings.

## Referecne

- [LINK](https://blogd.org/ai/reference/)
