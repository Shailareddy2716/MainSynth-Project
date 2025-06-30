## Overview

MemoSynth-Lite is a lightweight yet powerful AI-driven memory system designed to emulate human-like organizational memory. It integrates semantic understanding, graph-based reasoning, and chronological tracking to offer a comprehensive solution for storing, querying, summarizing, and analyzing organizational knowledge.

## Why JSON for Initial Memory Data?

For demonstration purposes, memory ingestion is handled through structured JSON files (`new_memories.json`) instead of live data sources. This approach allows:

* **Structured Representation**: Cleanly stores memory content, metadata, and tags.
* **Focus on Core Capabilities**: Highlights memory operations (storage, retrieval, summarization) without web scraping or parsing.
* **Ease of Use**: Easy to modify, share, and test sample memory data.

## Key Features

### Multi-Modal Memory Storage

* **Qdrant (Vector Database)**: Enables fast semantic search via embeddings.
* **Neo4j (Graph Database)**: Stores relationships between memory events (e.g., `related_to`, `caused_by`).
* **DuckDB (Timeline Database)**: Provides chronological logging and time-based querying.

### Hugging Face Integration (Local LLMs)

* **Embeddings**: Transforms summaries and queries into vectors using `sentence-transformers`.
* **Text Generation**: Local models power summarization, insight extraction, contradiction detection, and resolution.
* **Offline and Private**: Keeps data on-device with customizable, cost-effective local inference.

## Core Memory APIs

* `write_memory()`: Stores a memory across Qdrant, Neo4j, and DuckDB.
* `query_memory()`: Retrieves relevant memories using semantic similarity.
* `summarize_memories()`: Condenses memory content.
* `diff()`: Highlights differences between two memories.
* `resolve()`: Attempts to reconcile conflicting memories.
* `generate_insights()`: Extracts insights from a memory collection.

## Memory Schema

Memories are structured as JSON objects with metadata such as:

* `id`
* `project`
* `summary`
* `tags`
* `source`
* `timestamp`
* `confidence`

## Project Structure

```
.
├── app.py                          # Main application script
├── Assets/                         # Images and Result pdf
│   ├── Neo4J-Relationships.png
│   ├── Streamlitdashboard.png
│   ├── Result              
│   
├── build/                          # Build artifacts (ignored by Git)
├── docker-compose.yml              # Docker config for Qdrant and Neo4j
├── memory_timeline.db              # DuckDB timeline store
├── memosynth/                      # Core memory system modules
│   ├── __init__.py
│   ├── graph_store.py              # Neo4j integration
│   ├── huggingface_client.py       # LLM and embedding logic
│   ├── memory_client.py            # Main memory operations
│   ├── timeline_store.py           # DuckDB timeline handling
│   └── vector_store.py             # Qdrant interface
├── new_memories.json               # Demo memory dataset
├── notebook/
│   └── Demo.ipynb                  # Jupyter notebook demo
├── README.md                       # Project documentation
├── requirements.txt                # Python dependencies
├── setup.py                        # Package configuration
├── Taskfile.yaml                   # Task automation
├── test/
│   └── test_neo4j_connection.py    # Test Neo4j connectivity
```

## Getting Started

### Prerequisites

* Python 3.9+
* Git
* Docker & Docker Compose

### Installation

```bash
git clone <repository_url>
cd MemoSynth-Project
python3 -m venv venv
source venv/bin/activate  # On Windows: .\venv\Scripts\activate
pip install -r requirements.txt
pip install -e .
```

### Start Services (Qdrant & Neo4j)

```bash
docker-compose up -d
```

* Qdrant: [http://localhost:6333](http://localhost:6333)
* Neo4j: [http://localhost:7474](http://localhost:7474)

> **Note**: Default credentials are `neo4j/test1234`. Update `graph_store.py` if needed.

### Run the Demo Notebook

```bash
jupyter notebook
```

* Open `notebook/Demo.ipynb`
* Set `project_root = "/path/to/your/project"`
* Run all cells to see memory loading, querying, summarizing, resolving, and insights.
**Important**: The demo uses mocked LLM responses for stability.

### Run the App

```bash
streamlit run app.py
```

## Functional Demo Highlights

* **Memory Ingestion**
* **Semantic Querying**
* **Summarization**
* **Comparison (diff)**
* **Conflict Resolution (resolve)**
* **Insight Generation**

## Visual Assets

* **Neo4j Relationships**: Memory graph visualization
* **Result** This document summarizes the execution of a memory management system, featuring memory creation, querying, summarization, insight extraction, and comparison.
* **Streamlit Dashboard**: Interactive UI (future enhancement)

## Future Enhancements
**Richer Graph Relationships:** Automatically inferring and creating more complex relationships between memories (e.g., CAUSED_BY, HAS_ACTOR, PART_OF_EVENT) in Neo4j.

**User Interface:** Developing a simple web-based UI for interacting with the memory system.

**Scalability:** Optimizing for larger datasets and higher query loads.

