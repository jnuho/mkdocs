---
draft: false
date: 2024-08-18
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

<img src="https://docs.aws.amazon.com/images/sagemaker/latest/dg/images/jumpstart/jumpstart-fm-rag.jpg" target="_blank" width=550>

<sub><i>The following diagram shows the conceptual flow of using RAG with LLMs.: Original image credited to aws.amazon.com</i></sub>

<!-- more -->

<p align="left"><strong>Date:</strong> Auguest 20, 2024<br></p>

# What is Retrieval-Augmented Generation (RAG)?

Foundation model is trainined offline and is agonostic to any newly created data. This makes them less effective for domain-specific tasks. You can use Retrieval-Augmented Generation (RAG) pipeline to retrieve data from outside a foundation model and augment your prompts by adding the relevant retrieved data in context. 

RAG (Retrieval-Augmented Generation) combines the strengths of traditional **information retrieval** systems (such as databases) with the capabilities of generative large language models (LLMs) to produce more accurate and contextually relevant outputs.

The information retrieval utilizes the user input to first pull information from a new data source (authoritative, pre-determined knowledge sources). The user query and the relevant information are both given to the LLM. The LLM uses the new knowledge and its training data to create better responses. RAG uses benchmarks like Retrieval-Augmented Generation Benchmark (`RGB`) and `RAGTruth` to test and reduce hallucinations.

- Create external data
    - AI technique, called *embedding language models*, converts data into numerical representations and stores it in a vector database. This process creates a knowledge library that the generative AI models can understand.
- Retrieve relevant information
    - The next step is to perform a relevancy search. The user query is converted to a vector representation and matched with the vector databases. The system will retrieve relevant documents alongside the individual person's past record. The relevancy was calculated and established using mathematical vector calculations and representations.
    - **Reciprocal Rank Fusion (RRF)** can be used to improve the relevancy of search results by combining the rankings from multiple retrieval methods or models.
- Augment the LLM prompt
    - Next, the RAG model augments the user input (or prompts) by adding the relevant retrieved data in context. This step uses prompt engineering techniques to communicate effectively with the LLM. The augmented prompt allows the large language models to generate an accurate answer to user queries.
- Update external data
    - To maintain current information for retrieval, asynchronously update the documents and update embedding representation of the documents.
 
 - Useful links about RAG:
    - [LINK](https://blogd.org/ai/reference/)

## Reciprocal Rank Fusion (RRF)

- Various Retrieval Method
    - Reciprocal Rank Fusion (RRF)
    - Dense Retrieval with Transformers
    - BM25

Reciprocal Rank Fusion is a rank aggregation method that combines rankings from multiple sources into a single, unified ranking. In the context of RAG, these sources typically use different retrieval models or approaches.

The core of RRF is captured in its formula:

$$RRF(d) = \sum_{r \in R} \frac{1}{k + r(d)}$$

- d is a document
- R is the set of rankers (retrievers)
- k is a constant (typically 60)
- r(d) is the rank of document d in ranker r

1.  User Query: The process begins when a user inputs a question or query.
2.  Multiple Retrievers: The query is sent to multiple retrievers. These could be different retrieval models (e.g., dense, sparse, hybrid).
3.  Individual Rankings: Each retriever produces its own ranking of relevant documents.
4.  RRF Fusion: The rankings from all retrievers are combined using the RRF formula.
5.  Final Ranking: A unified ranking is produced based on the RRF scores.
6.  Generation: The generative model uses the top-ranked documents to produce the final answer.


## Text Embedding

- [sbert document](https://sbert.net/#)
- [sbert thesis](https://arxiv.org/pdf/1908.10084)


In the context of language models, text embedding is a technique where words, sentences, or even entire documents are transformed into high-dimensional vectors. These vectors capture semantic information about the text, enabling the model to understand and process language more effectively and allowing for more effective search and retrieval.

In an information retrieval system, text embedding is used to match a user's query with the most relevant entries in the database. By comparing vector representations, the system can identify which documents are most semantically similar to the query, even if the exact words used in the query do not appear in the documents.


## Vector Database in RAG

A text embedding model (like those provided by BERT, GPT, or other transformer-based models) converts text into high-dimensional vectors (numerical representations). These embeddings capture the semantic meaning of the text in a form that can be processed mathematically.

Vector databases are specialized for storing and managing these high-dimensional vectors. They are designed to efficiently perform similarity searches and nearest-neighbor searches, which are essential for applications involving embeddings.

## Referecne

- [LINK](https://blogd.org/ai/reference/)
