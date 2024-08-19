---
draft: false
date: 2024-08-18
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

<img src="https://d17pwbfgewyq5y.cloudfront.net/aiscope.png" target="_blank" width=300>

<p align="left"><strong>Date:</strong> Auguest 18, 2024<br></p>

# What is LLM?

Large Language Model (LLM), a subset of Generative AI, is a type of AI model specifically designed to understand, generate, manipulate <i>human language.</i> They are trained on vast amounts of text data and use this training to predict and generate text.

## Self-supervised learning

 Self-supervised learning

LLM is primarily trained using a form of self-supervision. It does not require explicit labels or annotations; instead, the model generates its own labels based on the data itself.

During training, the model sees part of a sentence and tries to predict the next word or fill in missing words (like in masked language modeling). The model can learn from large amounts of unstructured data, capturing a broad range of linguistic patterns and knowledge.

## Generative AI

Generative AI encompasses more than just language. It includes any AI that can create new content across different domains. LLMs are a specific application of Generative AI focused on language, specialized in generating and working with text.

## Foundation Model

Foundation model is a large, pre-trained model that serves as a base or "foundation" for a wide variety of downstream tasks. These models are trained on broad and diverse data, making them versatile for multiple applications. GPT-3 and GPT-4 are foundation models because they are pre-trained on vast amounts of data and can be fine-tuned or adapted for specific tasks, such as translation, summarization, sentiment analysis, and more.

LLMs are built from the Foundation Models and go through fine-tuning process during which the model's parameters are adjusted based on the new data, which might include domain-specific texts, dialogue examples, or other tailored content. ChatGPT, Gemini or Copilot are LLMs that are the fine-tuned versions of foundation models. 

## Three Pillars of LLM

LLMs excel in understanding and generating human language, enabling them to perform various language-related tasks such as translation, summarization, and content generation with high accuracy.

### 1. LARGE

- Scale of Data: LLMs are trained on vast amounts of text data
- Model Size: LLMs' architecture involves many parameters, often in the billions. 

### 2. LANGUAGE

- Understanding and Generation: LLMs are designed to comprehend and generate human language.
- Multilingual Capabilities: Many LLMs are trained on data from multiple languages, allowing them to understand and generate text in various languages, making them versatile tools for global applications.

### 3. MODELS

- Deep Learning Architectures: LLMs are built on advanced neural network architectures, such as <a href="https://www.youtube.com/watch?v=SZorAJ4I-sA" target="_blank"><b>transformers</b>.</a> (check [article](https://poloclub.github.io/transformer-explainer/?utm_source=tldrai))

- Transfer Learning: LLMs utilize transfer learning, where a pre-trained model on a large corpus is fine-tuned for specific tasks. 


## What are hallucinations in LLMs?

LLMs are powerful, but they're not without their shortcomings, as demonstrated by [incident](https://www.theverge.com/2023/2/8/23590864/google-ai-chatbot-bard-mistake-error-exoplanet-demo) of Bard's factual error in first demo. The point is when LLMs produce undesired output, it's called a — "hallucination" by the consensus. (Some says it is more like a glitch or bug.)


### Practices to Reduce Hallucinations in LLMs

Known challenges of LLMs include: presenting false information when it does not have the answer and creating inaccurate responses due to terminology confusion, etc.

Let's look at some of the key strategies that can be used to reduce LLM hallucinations: Fine-tuning LLMs, RAG, etc.

- Fine-Tunning LLMs
- Retrieval-Augmented Generation (RAG)

### Fine-Tuning LLMs

- Fine-tuning is a method in deep learning when a pre-trained model is further trained on a specific, often smaller, dataset to adapt it to a particular task or domain.
- Fine Tuning reduces hallucinations in LLMs by adjusting the model's patterns
- using curated data to align with specific contexts, improving factual accuracy and coherence.

### Retrieval-Augmented Generation (RAG)

- [LINK](https://blogd.org/deeplearning/RAG/)

### Reciprocal Rank Fusion (RRF)

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


### Text Embedding

In the context of language models, text embedding is a technique where words, sentences, or even entire documents are transformed into high-dimensional vectors. These vectors capture semantic information about the text, enabling the model to understand and process language more effectively and allowing for more effective search and retrieval.

In an information retrieval system, text embedding is used to match a user's query with the most relevant entries in the database. By comparing vector representations, the system can identify which documents are most semantically similar to the query, even if the exact words used in the query do not appear in the documents.


### Vector Database in RAG

A text embedding model (like those provided by BERT, GPT, or other transformer-based models) converts text into high-dimensional vectors (numerical representations). These embeddings capture the semantic meaning of the text in a form that can be processed mathematically.

Vector databases are specialized for storing and managing these high-dimensional vectors. They are designed to efficiently perform similarity searches and nearest-neighbor searches, which are essential for applications involving embeddings.


## Referecne

- [LINK](https://blogd.org/deeplearning/reference/)