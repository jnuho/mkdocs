---
draft: false
date: 2024-10-09
categories:
  - Deep Learning
  - LLM
authors:
  - junho
---

<img src="https://raw.githubusercontent.com/dleemiller/WordLlama/refs/heads/main/wordllama.png" target="_blank" width=250>

<sub><i>Original image credited to dleemiller/WordLlama</i></sub>

<!-- more -->
# Offline Model Usage and Optimization

## Initial Challenges

To use offline models, you need to download model parameters and configuration files from a remote hub. For example, when you use one of the languages models from Hugging Face, the respective model loading methods might download the model files into the cache directory. (e.g., `~/.cache/huggingface/hub/` or `~/.cache/wordllama/`, etc)


```python
from wordllama import WordLlama

# download default l2_supercat model
WL = WordLlama.load()
```

This means:

- Internet connection and HTTP communication are required when first loading the model.
- Download speed can take over over a minute for initial model download.
- Server slowdowns occur when starting or scaling up, due to model downloads and model loading.
- Increasing GPU specs to solve Cold Start latency also increases costs.
- When Cold start time triples, operational costs rise rapidly.

## Possible Improvement Methods

To address the challenges mentioned above, we explored several optimization techniques. Here are two key methods that proved effective:

### 1. Pre-downloading Models to Local Path

- Option to pre-download models locally when calling functions.
- Without this option, constant checks to the remote hub slow down model loading.
- Pre-downloaded model loading time: ~1.5 seconds (more than 2x faster than the original 4 seconds).
- After initial download, models can be loaded locally without internet connection.

### 2. Using Smaller Language Models

- Model size varies based on the number of parameters.
- Larger models have higher computation costs but increased accuracy.
- For our feature extraction, the minimized model (gliner_small) passed over 180 test cases with 100% accuracy.

**Result**: Using offline language models with local caching and lightweight models improved model loading speed by over 50%.

## Server Reliability and Monitoring

- Using Prometheus as a monitoring tool.
- Tracking which language models are used for feature extraction and where latency occurs.
- Metrics are recorded at the `/metrics` endpoint.
- Future plans include real-time visualization using tools like Grafana.

## Binary Quantization

Binary Quantization compresses vectors by reducing each dimension to a single bit (0 or 1). This means an n-dimensional vector of floating-point numbers is compressed to an n-dimensional vector of bits.


https://huggingface.co/blog/embedding-quantization


Since this method exploits the over-parameterization of embedding, you can expect poorer results for small embeddings i.e. less than 1024 dimensions. With the smaller number of elements, there is not enough information maintained in the binary vector to achieve good results.

https://qdrant.tech/articles/binary-quantization/



