# RAG
This Repository is related to projects on Retrieval Augmented Generation (RAG)

## Create virtual envrionment

```
conda create -n rag_env python=3.10

conda activate rag_env

pip3 install -r requirements.txt

```

## Problem Statement:

This project demonstrates **Retrieval-Augmented Generation (RAG)** by answering questions using **two external data sources**. The external data consists of AI-generated documents designed to simulate a realistic enterprise use case:

- [ElectroTV.pdf](sample_docs/ElectroTV.pdf) - A PDF product catalog for a **fictional electronic television brand named ElectroTV**

- [ElectroTV_Sales_Report_2024.csv](sample_docs/ElectroTV_Sales_Report_2024.csv) - A CSV sales report containing transactional sales data

The primary objective of this project is to start with a **Naive RAG** approach and progressively explore **advanced RAG techniques**, analyzing how each enhancement improves response quality, completeness, and reliability.

The question set is intentionally designed with **varying difficulty levels (easy, medium, and hard)**. While some questions are straightforward factual lookups, others require long-context understanding, cross-document reasoning, and numerical analysis, exposing the limitations of simpler RAG approaches.

Finally, the project aims to systematically evaluate and compare different RAG strategies, highlighting their strengths, weaknesses, and suitability for real-world applications involving both unstructured (PDF) and structured (CSV) data.

## Notebooks:

- [01_naive_rag.ipynb](01_naive_rag.ipynb)

- [02_agentic_rag.ipynb](02_agentic_rag.ipynb)

