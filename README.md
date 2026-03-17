# Ontology-Constrained-Retrieval-for-Historical-RAG
Experimental implementation of Ontology-Constrained Retrieval for historical RAG experiments on Wikidata.

This repository contains the experimental code used in the paper:

## Overview

The project compares three retrieval configurations:

1. Semantic Vector Retrieval (SVR)
2. Ontology-Guided Retrieval (OGR)
3. Fully Ontology-Constrained Retrieval (FOCR)

The goal is to evaluate how ontological constraints reduce retrieval noise before LLM generation.

## Repository Structure

- `core_vector_graph.py`: core retrieval logic
- `run_vector_graph.py`: experiment runner
- `data/tabella_short.csv`: short results table used in the paper
- `docs/pipeline_diagram.png`: pipeline figure

## Requirements

Python 3.10+

Install dependencies with:

```bash
pip install -r requirements.txt
