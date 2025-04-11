# GraphRAG vs. RAG for Math Textbook Page-level Retrieval and Question Answering

This repository contains code and data for the paper "What is the reference page number? Comparing RAG and GraphRAG for Page-level Retrieval Question Answering on Math Textbook."

## Overview

This project investigates Retrieval-Augmented Generation (RAG) and GraphRAG approaches for page-level question answering in mathematics textbooks. We focus on whether these methods can correctly identify the specific textbook page relevant to a given question, as well as generate high-quality answers.

Our study uses a custom dataset of 477 question-answer pairs derived from the undergraduate mathematics textbook "An Infinite Descent into Pure Mathematics" by Clive Newstead.

## Repository Structure

The repository is organized into four main components:

### 1. Textbook OCR and Content Extraction
Directory: `1_textbook-OCR-extract-content/`

This folder contains code for extracting and processing textbook content:
- `0_extract_pdf_to_png.ipynb`: Converts PDF pages to PNG images
- `1_png_to_markdown_create_batch_input.ipynb`: Prepares images for OCR processing
- `1.1_png_to_markdown_collect_batch_input_result.ipynb`: Collects OCR results
- `2_read_result.ipynb`: Processes OCR results into usable format
- `textbook.pdf`: Source textbook file
- Output files in markdown and JSON formats

### 2. QA Dataset Creation
Directory: `2_QA-data-creation/`

This folder contains the dataset creation pipeline:
- `data_math_gen.ipynb`: Code to generate question-answer pairs from textbook content
- `math_qa_all_v0.json` and `math_qa_all_v1.json`: Generated QA datasets

### 3. RAG Evaluation
Directory: `3_RAG_evaluation/`

This folder contains code for evaluating embedding-based RAG approaches:
- `test_retrieval/`: Evaluation of retrieval accuracy
- `test_reranker/`: Code for testing LLM reranking
- `test_generation/`: Evaluation of answer generation quality
- `test_mathRAG.ipynb` and variants: Main evaluation notebooks
- `math_qa.json`: The dataset used for evaluation
- `baseline.ipynb`: Evaluation of baseline approaches

### 4. GraphRAG Evaluation
Directory: `4_GraphRAG_evaluation/`

This folder contains code for evaluating the GraphRAG approach:
- `GraphRAG/`: Implementation and adaptation of GraphRAG
- `Baseline/`: Baseline comparisons

## Key Features

1. **Dataset Creation**: We generate and curate 477 question-answer pairs, each tied to a specific textbook page.

2. **Multiple RAG Approaches**:
   - Standard embedding-based RAG with various embedding models
   - GraphRAG using entity-relation extraction and graph structure

3. **Comprehensive Evaluation**:
   - Retrieval accuracy (whether the correct page is retrieved)
   - Answer quality (F1 score comparing generated answers to ground truth)
   - LLM-based reranking experiments

## Main Findings

1. Embedding-based RAG achieves higher retrieval accuracy and better F1 scores compared to GraphRAG.

2. Top-performing embedding models:
   - `voyage-3-large` achieves the highest retrieval accuracy
   - `nvidia/nv-embed-v2` achieves the best F1 scores for answer generation

3. GraphRAG tends to retrieve excessive content (~47K tokens per query vs. ~3.7K for standard RAG), affecting generation quality.

4. LLM-based reranking shows mixed results, with potential for hallucination in larger context windows.

## Usage

### Dataset Creation
```bash
# Extract content from textbook
cd 1_textbook-OCR-extract-content
jupyter notebook 0_extract_pdf_to_png.ipynb

# Generate QA pairs
cd ../2_QA-data-creation
jupyter notebook data_math_gen.ipynb
```

### Evaluation
```bash
# Evaluate embedding-based RAG
cd 3_RAG_evaluation
jupyter notebook test_mathRAG.ipynb

# Evaluate GraphRAG
cd 4_GraphRAG_evaluation/GraphRAG
# Follow instructions in the GraphRAG directory
```

## Dependencies

- Python 3.8+
- PyTorch
- Transformers
- Sentence-Transformers
- OpenAI API
- Jupyter Notebook
- GraphRAG (modified version)

## Citation

If you use this code or the dataset in your research, please cite our paper:

```
[Anonymous]
```
