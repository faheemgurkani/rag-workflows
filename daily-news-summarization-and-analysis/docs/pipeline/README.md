# Daily News Summarization and Analysis - RAG Pipeline

## Project Overview

This project implements a **Retrieval-Augmented Generation (RAG)** pipeline for daily news summarization and keyword-based analysis. It combines web scraping, keyword extraction, vector search, and Large Language Model (LLM) capabilities to generate insightful, grounded news summaries.

## Pipeline Architecture

The system operates through the following stages:

### 1. News Retrieval & Scraping

* **Tools**: `requests`, `BeautifulSoup`
* **Functionality**:

  * Fetches daily news articles from online sources based on customizable queries.
  * Supports Boolean operators like `AND`, `OR`, `NOT` for precise filtering.
  * Extracted fields include title, source, publication date, and content.
  * Saves the results to structured CSV files.

### 2. Data Ingestion & Preprocessing

* **Tools**: `pandas`, `os`, `dotenv`
* **Functionality**:

  * Loads saved news articles from CSV files.
  * Prepares textual data for embedding and semantic processing.

### 3. Keyword Extraction

* **Tools**: `KeyBERT`
* **Functionality**:

  * Extracts significant keywords and phrases from each news article.
  * Facilitates topical analysis and enhances search relevance.

### 4. Semantic Search with FAISS

* **Tools**: `faiss`, `numpy`, `sentence-transformers`
* **Functionality**:

  * Generates dense embeddings for news articles using `SentenceTransformer`.
  * Builds a FAISS vector index for efficient similarity search.
  * Enables fast retrieval of contextually relevant articles.

### 5. Retrieval-Augmented Generation (RAG)

* **Tools**: `openai`, `langchain`, `PromptTemplate`, `ChatOpenAI`
* **Functionality**:

  * Retrieves top relevant articles from FAISS based on user queries.
  * Constructs prompts by combining user input with retrieved context.
  * Utilizes OpenAI's LLM via LangChain to generate summaries or insights.
  * Ensures responses are grounded in factual retrieved content.

### 6. Additional Processing Features

* **Language Detection**: Uses `langdetect` to handle multilingual news sources.
* **Text Formatting**: Implements `textwrap` for clean console or file outputs.
* **Fuzzy Matching**: Applies `fuzzywuzzy` to compare and validate text similarity.
* **NLP Utilities**: Includes `spacy` for linguistic processing (optional).

## Technology Stack

| Category              | Tools/Packages                    |
| --------------------- | --------------------------------- |
| Web Scraping          | `requests`, `BeautifulSoup`       |
| Data Handling         | `pandas`, `os`, `dotenv`          |
| NLP & Text Processing | `spacy`, `langdetect`, `textwrap` |
| Keyword Extraction    | `KeyBERT`                         |
| Semantic Embeddings   | `sentence-transformers`           |
| Vector Search         | `faiss`, `numpy`                  |
| String Matching       | `fuzzywuzzy`                      |
| LLM & RAG Framework   | `openai`, `langchain`             |

## Setup Instructions

1. **Install Dependencies**

   ```bash
   pip install -r requirements.txt
   python -m spacy download en
   ```
2. **Environment Variables**

   * Create a `.env` file with necessary API keys, e.g.:

     ```
     OPENAI_API_KEY=your_openai_key_here
     ```

## Usage Guide

* Run the notebook step-by-step:

  1. Scrape or load news articles.
  2. Perform keyword extraction.
  3. Build the FAISS index.
  4. Enter queries to retrieve and summarize relevant news.

## Example Workflow

```python
news_fetcher = NewsFetcher(api_key="...")
news_fetcher.fetch_news(query="Tech AND AI")
news_fetcher.save_to_csv("daily_news.csv")

indexer = NewsIndexer("daily_news.csv")
indexer.build_index()

rag_agent = NewsRAG(indexer)
summary = rag_agent.query("Latest AI breakthroughs")
print(summary)
```

## Conclusion

This system provides an end-to-end pipeline for automating news monitoring, summarization, and topical analysis using modern RAG techniques grounded in LLM and vector search capabilities.
