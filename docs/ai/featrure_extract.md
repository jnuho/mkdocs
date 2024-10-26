---
draft: false
date: 2024-09-23
categories:
  - LLM
authors:
  - junho
---

I leanred NLP techniques for feature extraction. In this post I will dive into text embedding models for feature extraction.

<!-- more -->

https://github.com/edmissionai/edmission/pull/144

I tested performance of feature extraction with NLP vs. GLiNER + WordLlamma. GLiNER and WordLlama use small offline text embedidng models from hugging face. They are fast relative to large models like SBERT. I achieve over 90% of speed of NLP (343ms/test) techniques. Each takes less than .5 seconds so this is not a huge of a difference.

Using sbert takes over 1-2 seconds. So these small models are faster without decline in accuracy of feature extraction. (I performed unittest with 122 test cases.)

- [feat(optimize): remove and optimize db calls](https://github.com/edmissionai/edmission/pull/146)
- offline model extract improved by loading db data during class initialization in init for multiple use
    - 10% speed increase : 333 ms / test -> 297 ms / test
    - 122 test cases now run 10% faster (for offline feature extraction)
    - define "select_all_official_names", "select_all_other_names"
## WordLlamma

https://github.com/dleemiller/WordLlama



## GLiNER

https://github.com/urchade/GLiNER
