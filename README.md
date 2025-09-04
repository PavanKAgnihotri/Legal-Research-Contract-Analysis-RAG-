# Legal-Research-Contract-Analysis-RAG-

This project demonstrates building a Retrieval Augmented Generation (RAG) system for legal research and contract analysis. It involves ingesting data from multiple legal sources (CourtListener, CUAD contracts, and U.S. Code), creating a vector store using FAISS for efficient retrieval, and using a Gemini model for generating answers based on the retrieved information. A Gradio interface is included for interacting with the system.

Prerequisites

Google Account and API Key: You need a Google account and a Google Cloud project with the Generative AI API enabled to use the Gemini models for embeddings and chat.

API Token for CourtListener: To ingest data from CourtListener, you'll need an API token. The current code has a hardcoded token, but it's recommended to use environment variables or Colab secrets for security.

Access to Data Files: The notebook assumes you have access to the following data files, preferably stored in your Google Drive and mounted in Colab:
  CourtListener data (ingested directly via API).
  CUAD dataset in JSON format (CUAD_v1.json).
  U.S. Code data in XML format (US_Code directory with XML files).

Python Libraries: The notebook requires the installation of several Python libraries, including langchain, langchain-community, faiss-cpu, and jsonlines. The first code cell handles these installations.

Workflow
The notebook follows these main steps:

Setup: Installs necessary libraries and defines configurations like API keys and data paths.

Data Ingestion:
  Fetches data from the CourtListener API.
  Loads and preprocesses the CUAD JSON dataset.
  Parses and preprocesses U.S. Code XML files.
  Saves the preprocessed data as JSONL files.

Embedding, Chunking, and Indexing:
  Uses the GoogleGenerativeAIEmbeddings model to create vector representations of the text data.
  Splits the documents into smaller chunks using RecursiveCharacterTextSplitter.
  Builds separate FAISS vector stores for each data source (CourtListener, CUAD, U.S. Code).
  Saves the FAISS indices locally.

Retrieval and Generation:
  Loads the saved FAISS indices.
  Implements a routing mechanism (using Gemini or keyword fallback) to determine which data source(s) are relevant to a user query.
  Retrieves relevant document chunks from the selected vector store(s) using similarity search.
  Uses a ChatGoogleGenerativeAI model to generate an answer based on the user query and the retrieved context.

Gradio Interface: Sets up a simple Gradio chatbot interface to interact with the RAG system.
