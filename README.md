## Helpmate AI - An RAG based information retrieving model tested on a Health Isurance document ##

This code file contains a simple starter notebook for the HelpMate AI project

### Problem Statement: ###

The goal of the project is to build a RAG system using frameworks such as
LangChain and Ollama to retrieve information from any document by asking questions.


### Here’s how we have implemented the RAG with the following tools: ###
-LangChain -- A framework for building applications with LLMs that enables
-chaining tasks, retrieval, and external data integrations.
-Ollama (Version-3.2) -- The OpenAI LLM API to generate responses using GPT models.
-Embeddings (HuggingFace)
-Vector Database (FAISS)
-Pdfplumber was used for chunking the data

### Data Preparation ###
-Ingest Data: The data we want our system to access was collected (PDFs, web pages or
tables) and the text was split into chunks for better retrieval.
-Generate Embeddings: Used a pre-trained embedding model to convert textual data into vector
embeddings and stored these in a vector database.

### Building the Retrieval Pipeline ###
-Used LangChain’s Retrieval Tools to interact with the vector database.
-Implemented a retriever like VectorStoreRetriever to search the database for
relevant documents using cosine similarity.

### RAG Pipeline ###
-Passed the query to the retriever, which fetches relevant documents based on
similarity.
-Combined retrieved documents with the original query.
-Used OLAMA to process the augmented input and generate a response.

### Explanation of Key Components: ###
-Document loader: -- PDFPlumberLoader(): It handles various PDF formats,
including multi-page, scanned, and text-heavy documents.
-Text Splitter: -- RecursiveCharacterTextSplitter(): It is a utility in LangChain
that breaks large pieces of text (like documents) into smaller, manageable
chunks.
-Embeddings -- (HuggingFace): It offers an alternative to OpenAI’s
embeddings and can run locally without requiring API calls. These embedding
models are used to convert text into numerical vectors.
-Vector Database -- (FAISS): It efficiently searches for similar embeddings in large datasets and used for storing 
and retrieving embeddings of documents or data.
- Retriever -- retriever(): Queries the FAISS store to fetch top-k relevant chunks.-
- OpenAI LLM – using llama3.2 version : Combines the query and retrieved chunks to generate a coherent response.

### Challenges faced: ###
Incorrect Data Retrieval from Tables
- Extracting data from tables in PDFs was problematic, leading to misaligned or
incomplete information.
-Tables with complex structures, such as merged cells or multi-page formats,
were not processed correctly.

### Solution: ###
-Improved Chunking Strategy Using pdfplumber
-Replaced PDFLoader with pdfplumber, which provided better table extraction
capabilities.
-Implemented a revised chunking strategy to preserve table structure and
improve data accuracy.
-Successfully retrieved genetic sequencing data with correct formatting,
enhancing data reliability and downstream analysis.
