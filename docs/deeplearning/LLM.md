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

Large Language Model (LLM) is a subset of deep learning and Generative AI. LLM is a type of AI model specifically designed to understand, generate, manipulate <i>human language.</i> They are trainined on vast amounts of text data and use this training to predict and generate text.

## Self-supervised learning

LLM is primarily trained using a form of self-supervision. It does not require explicit labels or annotations; instead, the model generates its own labels based on the data itself.

During training, the model sees part of a sentence and tries to predict the next word or fill in missing words (like in masked language modeling). The model can learn from large amounts of unstructured data, capturing a broad range of linguistic patterns and knowledge.

## Generative AI

Generative AI encompasses more than just language. It includes any AI that can create new content across different domains. LLMs are a specific application of Generative AI focused on language, specialized in generating and working with text.

## Foundation Model

A foundation model is a large, pre-trained model that serves as a base or "foundation" for a wide variety of downstream tasks. These models are trained on broad and diverse data, making them versatile for multiple applications. LLMs like GPT-3 and GPT-4 are foundation models because they are pre-trained on vast amounts of data and can be fine-tuned or adapted for specific tasks, such as translation, summarization, sentiment analysis, and more.

You've probably heard of ChatGPT, Gemini or Copilot. They are examples of fine-tuned versions of foundation models. They are LLMs that are built from the Foundation Models and go through fine-tuning process during which the model’s parameters are adjusted based on the new data, which might include domain-specific texts, dialogue examples, or other tailored content.

A foundation model can be employed to develop a chatbot, translate languages, or craft creative content. In contrast, LLMs are usually specialized for one or two specific functions, like text generation or language translation. Whilst foundation models are used for a broader spectrum of output, they’re a bit undercooked. LLMs on the other hand, are more developed and stable, in that their accuracy rate is better than foundation models.


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

LLMs are powerful, but they’re not without their shortcomings, as demonstrated by [incident](https://www.theverge.com/2023/2/8/23590864/google-ai-chatbot-bard-mistake-error-exoplanet-demo) of Bard's factual error in first demo. The point is when LLMs produce undesired output, it’s called a — "hallucination" by the consensus. (Some says it is more like a glitch or bug.)


### Practices to Reduce Hallucinations in LLMs

Known challenges of LLMs include: presenting false information when it does not have the answer and creating inaccurate responses due to terminology confusion, etc.

Let’s look at some of the key strategies that can be used to reduce LLM hallucinations: Fine-tuning LLMs, RAG, etc.

- Fine-Tunning LLMs
- Retrieval-Augmented Generation (RAG)

### Fine-Tuning LLMs

- Fine-tuning is a method in deep learning when a pre-trained model is further trained on a specific, often smaller, dataset to adapt it to a particular task or domain.
- Fine Tuning reduces hallucinations in LLMs by adjusting the model’s patterns
- using curated data to align with specific contexts, improving factual accuracy and coherence.

### Retrieval-Augmented Generation (RAG)

RAG (Retrieval-Augmented Generation), an AI framework, to solve the challenges mentioned at the beginning. It combines the strengths of traditional information retrieval systems (such as databases) with the capabilities of generative large language models (LLMs) to produce more accurate and contextually relevant outputs. 

It <i>redirects the LLM to retrieve relevant information from authoritative, pre-determined knowledge sources.</i> Organizations have greater control over the generated text output, and users gain insights into how the LLM generates the response. It uses benchmarks like Retrieval-Augmented Generation Benchmark - `RGB` and `RAGTruth` to test and reduce hallucinations.

With RAG, an **information retrieval** component is introduced that utilizes the user input to first pull information from a new data source. The user query and the relevant information are both given to the LLM. The LLM uses the new knowledge and its training data to create better responses.

- Create external data
    - AI technique, called *embedding language models*, converts data into numerical representations and stores it in a vector database. This process creates a knowledge library that the generative AI models can understand.
- Retrieve relevant information
    - The next step is to perform a relevancy search. The user query is converted to a vector representation and matched with the vector databases. The system will retrieve relevant documents alongside the individual person's past record. The relevancy was calculated and established using mathematical vector calculations and representations.
    - **Reciprocal Rank Fusion (RRF)** can be used to improve the relevancy of search results by combining the rankings from multiple retrieval methods or models.
- Augment the LLM prompt
    - Next, the RAG model augments the user input (or prompts) by adding the relevant retrieved data in context. This step uses prompt engineering techniques to communicate effectively with the LLM. The augmented prompt allows the large language models to generate an accurate answer to user queries.
- Update external data
    - To maintain current information for retrieval, asynchronously update the documents and update embedding representation of the documents.
 
- Article on RAG from:
    - [AWS](https://aws.amazon.com/what-is/retrieval-augmented-generation/)
    - [Google cloud](https://cloud.google.com/use-cases/retrieval-augmented-generation)
    - [Oracle](https://www.oracle.com/artificial-intelligence/generative-ai/retrieval-augmented-generation-rag/)
    - [databricks](https://www.databricks.com/glossary/retrieval-augmented-generation-rag)

<img src="https://docs.aws.amazon.com/images/sagemaker/latest/dg/images/jumpstart/jumpstart-fm-rag.jpg" alt="gradient descent" width="650">

<sub><i>The following diagram shows the conceptual flow of using RAG with LLMs.: Original image credited to aws.amazon.com</i></sub>

### Retrieval Method

- BM25
- Reciprocal Rank Fusion (RRF)
- Dense Retrieval with Transformers

### Reciprocal Rank Fusion (RRF)

Reciprocal Rank Fusion is a rank aggregation method that combines rankings from multiple sources into a single, unified ranking. In the context of RAG, these sources typically use different retrieval models or approaches.

The core of RRF is captured in its formula:

$$RRF(d) = \sum_{r \in R} \frac{1}{k + r(d)}$$

- d is a document
- R is the set of rankers (retrievers)
- k is a constant (typically 60)
- r(d) is the rank of document d in ranker r

1. User Query: The process begins when a user inputs a question or query.
2. Multiple Retrievers: The query is sent to multiple retrievers. These could be different retrieval models (e.g., dense, sparse, hybrid).
3. Individual Rankings: Each retriever produces its own ranking of relevant documents.
4. RRF Fusion: The rankings from all retrievers are combined using the RRF formula.
5. Final Ranking: A unified ranking is produced based on the RRF scores.
6. Generation: The generative model uses the top-ranked documents to produce the final answer.


### Text Embedding

text -> vectored
In the context of language models, text embedding is a technique where words, sentences, or even entire documents are transformed into high-dimensional vectors. These vectors capture semantic information about the text, enabling the model to understand and process language more effectively and allowing for more effective search and retrieval.

In an information retrieval system, text embedding is used to match a user's query with the most relevant entries in the database. By comparing vector representations, the system can identify which documents are most semantically similar to the query, even if the exact words used in the query do not appear in the documents.


### Vector Database in RAG

A text embedding model (like those provided by BERT, GPT, or other transformer-based models) converts text into high-dimensional vectors (numerical representations). These embeddings capture the semantic meaning of the text in a form that can be processed mathematically.

Vector databases are specialized for storing and managing these high-dimensional vectors. They are designed to efficiently perform similarity searches and nearest-neighbor searches, which are essential for applications involving embeddings.


## Referecne

- [Eric Schmidt, AI Conference at Standford](https://www.youtube.com/watch?v=T_JKIkSf93Y)
- [Geoffrey Hinton: Will digital intelligence replace biological intelligence?](https://www.youtube.com/watch?v=iHCeAotHZa4)
- [Henrik Kniberg: Generative AI in a Nutshell](https://www.youtube.com/watch?v=2IK3DFHRFfw)
- [Emergent Garden: Why Neural Networks can learn (almost) anything](https://www.youtube.com/watch?v=0QczhVg5HaI)
- [Emergent Garden: Watching Neural Networks Learn](https://www.youtube.com/watch?v=TkwXa7Cvfr8)
- [Steve Brunton: Physics Informed Machine Learning](https://www.youtube.com/watch?v=JoFW2uSd3Uo)
- [How I became a machine learning practitioner](https://blog.gregbrockman.com/how-i-became-a-machine-learning-practitioner)
- [Gavin Uberti - Real-Time AI & The Future of AI Hardware](https://podcasts.apple.com/tw/podcast/gavin-uberti-real-time-ai-the-future-of-ai-hardware/id1154105909?i=1000638288111)
- [Michael Royzen: Beating GPT-4 with Open Source Models (Phind)](https://www.youtube.com/watch?v=z1rHPFiY6FA)
- [YC Combinator AI startup by college kids (2024)](https://www.youtube.com/watch?v=fmI_OciHV_8)
- [Sholto Douglas & Trenton Bricken - How to Build & Understand GPT-7's Mind](https://www.youtube.com/watch?v=UTuuTTnjxMQ)

<hr>

- [tldr tech](https://tldr.tech/)
- [Transformer explainer](https://poloclub.github.io/transformer-explainer/?utm_source=tldrai)
- Youtube
    - [AI, Machine Learning, Deep Learning and Generative AI Explained](https://www.youtube.com/watch?v=qYNweeDHiyU)
    - [The Rise of Generative AI - series](https://www.youtube.com/watch?v=s4r5gXdSVPM&list=PLOspHqNVtKACJx_ue2EXC1MerohY_lLKO)
    - [Generative AI in a Nutshell](https://www.youtube.com/watch?v=2IK3DFHRFfw&t=170s)
- [Make Your Own Neural Network](https://www.amazon.com/Make-Your-Own-Neural-Network/dp/1530826608)
- [Neural Networks From Scratch](https://nnfs.io/)
- [Understanding Deep Learning](https://udlbook.github.io/udlbook/)
- [Deep Learning: Foundations and Concepts](https://bishopbook.com/)
- [Zero to Mastery Learn PyTorch for Deep Learning](https://www.learnpytorch.io/)
- [LLMs from scratch](https://github.com/rasbt/LLMs-from-scratch)
- [Andrej Karpathy, intro to neural networks and backpropagation: building micrograd](https://www.youtube.com/watch?v=VMj-3S1tku0)
- [Diffusion models from scratch, from a new theoretical perspective](https://www.chenyang.co/diffusion.html)
- [3Blue1Brown: But what is a neural network?](https://www.youtube.com/watch?v=aircAruvnKk)
- [3Blue1Brown: Visualizing Attention, a Transformer's Heart](https://www.youtube.com/watch?v=eMlx5fFNoYc)
- [Mamba explained](https://thegradient.pub/mamba-explained/)
- [LLaMA Now Goes Faster on CPUs](https://justine.lol/matmul/)
- [Mamba-Palooza: 90 Days of Mamba-Inspired Research with Jason Meaux: Part 1](https://www.youtube.com/watch?v=Bg1LQ_jWliU)
- [Mamba-Palooza: 90 Days of Mamba-Inspired Research with Jason Meaux: Part 2](https://www.youtube.com/watch?v=MwIiQsEVyew)