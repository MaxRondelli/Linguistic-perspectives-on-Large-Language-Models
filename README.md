# Understanding Word Meanings in Context: An Investigation using Large Language Models

This repository contains the research work and implementation for investigating how Large Language Models (LLMs) understand and process word meanings in different contexts. The project specifically focuses on semantic analysis and polysemy, examining how well various LLMs can distinguish between different meanings of the same word in different contexts.

## Project Overview

The research explores three fundamental questions:
1. Can LLMs grasp word meanings and sentence context with human-like understanding?
2. How do LLMs perform when interpreting word meanings across different contexts?
3. What are effective methods for evaluating LLM performance in this domain?

## Linguistic Focus

Our investigation centers on semantic analysis and polysemy - the linguistic phenomenon where words have multiple related meanings sharing core semantic properties but different contextual usage. For example:

- The word "head" can mean:
  - A leader/person in charge: "She is the head of the department"
  - A physical body part: "He hit his head on the doorframe"

- The word "paper" can refer to:
  - An academic article: "The professor published a paper in Nature"
  - A physical material: "I need some paper to print these documents"

## Dataset

We utilized the Multilingual Word-in-Context (WiC) Dataset for our experiments. This dataset is specifically designed to evaluate LLMs' ability to disambiguate word meanings through binary classification:
- Label 1: Same meaning in both contexts
- Label 0: Different meanings

The dataset structure includes:
- target_word: The word being analyzed in both examples
- PoS: Part-of-Speech tag (N for noun, V for verb)
- start-index_i and end-index_i: Character indices for target word location
- example_i: Context sentences
- label: Binary classification (0/1)

## Implementation

### Models Evaluated

We analyzed 100 equally distributed samples across five different LLMs:
1. GPT-4-turbo (OpenAI)
2. GPT-4 (OpenAI)
3. GPT-3.5 (OpenAI)
4. Phi-3 (Microsoft)
5. llama-3.2 (Meta)

Access methods:
- OpenAI API for GPT models
- Ollama for Phi-3 and llama-3.2 (open-source models)

### Methodology

The models were evaluated using two distinct prompt templates:

Template 1: You are a helpful assistant. My goal is to check if a target word in a sentence has the same intended sense in another sentence. A target word and two sentences will be passed. Check if the intended sense is the same or not. Label as (1) if the meaning is the same, viceversa (0) for different meaning. In the final response you always add a line where you write the correct Label you think it is, starting in the following way: Label

Template 2: You are a linguistics expert. Determine if a given 'target word' has a same meaning in two sentences. Respond with 1 if the meaning of the word is similar or 0 if it is too different. Include your explanation, then write in new line 'Label: 1 or 0'

### Evaluation Metrics

We employed multiple evaluation metrics:
- Accuracy
- Precision
- Recall
- F1 score
- Confusion Matrix

### Embedding Analysis

We conducted detailed embedding analysis using:
- Principal Component Analysis (PCA) for dimensionality reduction
- Cosine similarity for comparing context embeddings

## Results

### Model Performance Metrics

| Model | Template | Accuracy | Precision | Recall | F1 Score |
|-------|----------|----------|-----------|---------|-----------|
| GPT-4 Turbo | T0 | 0.69 | 0.85 | 0.46 | 0.60 |
|             | T1 | 0.69 | 0.85 | 0.46 | 0.60 |
| GPT-4       | T0 | 0.65 | 0.78 | 0.42 | 0.55 |
|             | T1 | 0.73 | 0.73 | 0.72 | 0.73 |
| GPT-3.5     | T0 | 0.57 | 0.77 | 0.20 | 0.32 |
|             | T1 | 0.54 | 0.55 | 0.48 | 0.51 |
| Phi-3       | T0 | 0.54 | 0.67 | 0.16 | 0.26 |
|             | T1 | 0.65 | 0.65 | 0.64 | 0.65 |
| LLAMA 3.2   | T0 | 0.52 | 0.57 | 0.16 | 0.25 |
|             | T1 | 0.64 | 0.61 | 0.80 | 0.69 |

*Note: T0 and T1 represent Template 0 and Template 1 respectively.*

## References

- [WiC: the Word-in-Context Dataset](https://arxiv.org/pdf/1808.09121)
- [WiC Dataset Official Page](https://pilehvar.github.io/wic/)
- [Cosine Similarity for Word Embeddings](https://medium.com/@techclaw/cosine-similarity-between-two-arrays-for-word-embeddings-c8c1c98811b)
