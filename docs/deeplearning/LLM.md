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
- Retrieval-Augmented Generation (RAG): [LINK](https://blogd.org/deeplearning/RAG/)

### Fine-Tuning LLMs

- Fine-tuning is a method in deep learning when a pre-trained model is further trained on a specific, often smaller, dataset to adapt it to a particular task or domain.
- Fine Tuning reduces hallucinations in LLMs by adjusting the model's patterns
- using curated data to align with specific contexts, improving factual accuracy and coherence.





## Referecne

- [LINK](https://blogd.org/deeplearning/reference/)