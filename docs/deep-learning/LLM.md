---
draft: false
date: 2024-08-18
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

<p align="left"><strong>Date:</strong> Auguest 18, 2024<br></p>

# What is LLM

Large Language Model is a subset of deep learning and Generative AI. LLM is a type of AI model sepcifically designed to <i>understand, generate, manipulate human language.</i> They are trainined on vast amounts of text data and use this training to predict and generate text.

## Self-supervised learning

During training, the model sees part of a sentence and tries to predict the next word or fill in missing words (like in masked language modeling), thus a self-supervised learning: the model generates its own labels from the data based on the structure or inherent patterns within the data itself. The model can learn from large amounts of unstructured data, capturing a broad range of linguistic patterns and knowledge.


## Generative AI

Generative AI encompasses more than just language. It includes any AI that can create new content across different domains. LLMs are a specific application of Generative AI focused on language, specialized in generating and working with text.


## Foundation Model

Foundation models, such as GPT-3 and GPT-4, are trained on extensive and diverse datasets in a broad, general-purpose manner.

You've probably heard of ChatGPT, Gemini or Copilot. They are examples of fine-tuned versions of foundation models. They are LLMs that are built from the Foundation Models and go through fine-tuning process during which the model’s parameters are adjusted based on the new data, which might include domain-specific texts, dialogue examples, or other tailored content. This fine-tuning process helps the model refine its abilities and make it more effective for particular applications.

A foundation model is a large, pre-trained model that serves as a base or "foundation" for a wide variety of downstream tasks. These models are trained on broad and diverse data, making them versatile for multiple applications. LLMs like GPT-4 are foundation models because they are pre-trained on vast amounts of data and can be fine-tuned or adapted for specific tasks, such as translation, summarization, sentiment analysis, and more.

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


### Best Practices to Reduce Hallucinations in LLMs

- Retrieval-Augmented Generation (RAG)
    - Combines information retrieval with LLMs to produce accurate outputs.
    - Uses benchmarks like Retrieval-Augmented Generation Benchmark (RGB) and RAGTruth to test and reduce hallucinations.

- Fine-Tuning LLMs
    - Fine-tuning is a method in deep learning when a pre-trained model is further trained on a specific, often smaller, dataset to adapt it to a particular task or domain.
    - Fine Tuning reduces hallucinations in LLMs by adjusting the model’s patterns
    - using curated data to align with specific contexts, improving factual accuracy and coherence.

### Retrieval-Augmented Generation (RAG)

- Combines information retrieval with LLMs to produce accurate outputs.
- Uses benchmarks like Retrieval-Augmented Generation Benchmark (RGB) and RAGTruth to test and reduce hallucinations.




## Links



- Idea and Concept

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

- Reference

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