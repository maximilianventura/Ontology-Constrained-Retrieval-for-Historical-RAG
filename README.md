# Ontology-Constrained Retrieval for Historical RAG

Code accompanying the paper:

**Ontology-Constrained Retrieval for Historical RAG**

## Overview

This repository contains the experimental code used to compare two retrieval architectures:

1. Semantic Vector Retrieval (SVR)
2. Ontology-Constrained Retrieval (OCR)

The goal is to evaluate how structural constraints derived from Wikidata relations can reduce semantic noise in fact retrieval.

Unlike document-based RAG systems, this work operates on **atomic factual statements** extracted from Wikidata and represented as vector embeddings.

## Repository Structure

core_vector_graph.py  
Core retrieval logic.

run_vector_graph.py  
Script used to run the experimental configurations and reproduce the experiments.

requirements.txt  
List of Python dependencies required to run the experiments.

LICENSE  
Open source license for the code.

## Experimental Setup

The experiments operate on a dataset derived from Wikidata consisting of approximately **191,000 factual statements** related to the period **1400–1700**.

Each statement is represented as a structured record containing:

- source entity (SRC)
- relation (PID – Wikidata Property ID)
- destination entity (DST)
- optional temporal metadata
- natural language linearization of the fact

The statements are embedded using the model:

sentence-transformers/paraphrase-multilingual-MiniLM-L12-v2

and indexed in the **Qdrant vector database**.

## Retrieval Configurations

Two configurations are evaluated.

**SVR – Semantic Vector Retrieval**

Standard vector similarity search based purely on semantic proximity between query and statement embeddings.

**OCR – Ontology-Constrained Retrieval**

Vector retrieval combined with structural constraints derived from Wikidata relations and temporal metadata.  
These constraints restrict the search space and filter candidates that are structurally incompatible with the query.

## Example Usage

Example semantic retrieval:

python run_vector_graph.py --mode svr --q "Chi è nato a Milano nel 1489?"

Example ontology-constrained retrieval:

python run_vector_graph.py --mode ocr --q "Chi è nato a Milano nel 1489?"

## Requirements

Python 3.10+

Install dependencies with:

pip install -r requirements.txt

Main dependencies include:

- qdrant-client
- sentence-transformers
- pandas
- numpy

## Dataset Reconstruction

The dataset is **not distributed directly** because it is derived from Wikidata.

To reconstruct the dataset:

1. Extract entities and relations from Wikidata using SPARQL queries.
2. Convert statements into flat factual records containing SRC, PID, DST and temporal metadata.
3. Generate text linearizations of the facts.
4. Compute embeddings using SentenceTransformers.
5. Index the embeddings in Qdrant.

This process produces the experimental corpus of approximately **191,000 factual statements** used in the paper.

## Scope

This repository supports a **methodological experiment** on retrieval control in historical fact retrieval.

The goal is to study how structural constraints can reduce semantic noise before generation.  
It is not intended to provide a production-ready search system.
