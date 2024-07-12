# Tutorial-on-Advanced-RAG
Tutorial on Implementation of Advanced RAG system with Groq+Llama3, Qdrant Vector store, and Cohere Re-ranker


Advanced RAG refers to the implementation of RAG framework with enhanced information retrieval from external sources and improving generation of the LLMs. 
In this tutorial, we'll explore how to build an advanced RAG application using LLMs for generating, evaluating, and reranking responses. We'll leverage Groq’s LLAMA-3 8B model (for faster response generation), Qdrant for vector storage, and Cohere ReRanker for improving response quality. Additionally, we'll use LangChain to integrate these components seamlessly.
Advanced RAG has the following key aspects: 
1.	Multiple Query Expansion: 
o	Advanced RAG system generates multiple variations of the user’s initial query to have various interpretations, helping retrieve diverse and comprehensive set of information. 
o	LLM Integration: 
2.	Enhanced Retrieval: 
o	The systems use vector databases (such as Qdrant – as used in this tutorial) for efficient storage and retrieval of information. The retrieval also uses semantic similarity search using an embedding model. 
o	The system combines the most relevant documents to create a comprehensive context for LLM to work with. 
3.	Reranking: 
o	After retrieval, the Advaced RAG system employs reranking algorithms (such as Cohere’s reranker used in this turorial) to refine the search results, ensuring most relevant information is prioritized. 
4.	Multiple Response Generation: 
o	Instead of generating a single response, advanced RAG systems often produce multiple potential answers using the retrieved context
5.	Response Evaluation: 
o	The evaluation of the response is done based on Relevance, accuracy and completeness using the LLM or specialized methods. 
6.	Final Selection: 
o	The highest scored response is selected and presented to the user.    

Pre-requisites: 
Before getting started, ensure the following are met: 
-	Python installed on your machines
-	API keys – please proceed to sign-up and obtain the keys for the following:
o	ChatGroq
o	Qdrant – Copy URL and API Key
o	Cohere
-	Basic understanding of Open-source LLM inferencing, prompting and vector stores

Pre-requisites: 
Before getting started, ensure the following are met: 
-	Python installed on your machines
-	API keys – please proceed to sign-up and obtain the keys for the following:
o	[ChatGroq](https://console.groq.com/keys) - Create API Key
o	[Qdrant](https://qdrant.tech/documentation/cloud/authentication/) – Copy URL and API Key
o	[Cohere](https://dashboard.cohere.com/api-keys) – after creating an account, go to Cohere dashboard to create the API key
-	Basic understanding of Open-source LLM inferencing, prompting and vector stores
Setting the API Keys as Environment Variables: 
API keys are unique identifiers, and developers often need to protect these, as it can pose security risks if not managed properly. A common practice is to store these keys in environment variables. Here we use a Python library called `python-dotenv` to manage the environment variables. It will help host a `.env` file  to securely store the API keys and show how to access these values in Python programs. 
Step 1: Installing the library
	pip install python-dotenv
Step 2: Creating `.env` file in the root directory of our project. It is a file that stores key-value pairs, representing an environment variable and its value. 
```
GROQ_API_KEY = `your-groq-api-key`
QDRANT_API_KEY = `your-qdrant-api-key`
QDRANT_API_URL = `your-qdrant-url`
COHERE_API_KEY = `your-cohere-api-key`
```
Replace `your-groq-api-key`, `your-qdrant-api-key`, `your-qdrant-url`, `your-cohere-api-key`with your actual API keys.
NOTE: It is essential to add your .env file in your .gitignore file to ensure it doesn’t reflect in your version control system. 
Step 3: Open your `.gitignore` file (create one if it doesn’t exist). Add `.env` file on a new line and save the `.gitignore` file
Step 4: Now that we have setup our `.env` file, we will start using it in our Python code. 
```	
from dotenv import load_dotenv
load_dotenv()
```
In the tutorial, we will see how we use these stored API keys in the `.env` file for our application. 

Architecture Overview: 
This tutorial implements an Advanced RAG application with the following structured architecture as follows:
Model: Llama3-8B
Vector Database: Qdrant
Embedding Model: sentence-transformers/all-MiniLM-L6-v2 for relevant information search and retrieval 
Sample Dataset: Information on “Challenges in Quantum Computing” 
1.	Dataset: Create a sample dataset, or use your custom dataset for retrival of information. 
2.	Vector Store Setup: Utilize Qdrant for storing and retrieving vector representations. Add the content from your Dataset to the Qdrant vector store. 
3.	LLM Integration: Use Groq+Llama3 for generating queries and responses, based on the context provided. 
4.	Query Generation: Generate n queries (5 queries shown in this tutorial) using the LLM 
5.	Response Generation by Retrieval and Re-ranking: With the help of context stored in the vector database, generate relevant response for the different queries using the LLM. Re-ranking helps improve the response quality using the Cohere Re-ranker to help obtain higher semantic quality content. 
6.	Response Evaluation: Evaluation of the generated response with the LLM based on Relevance, Accuracy and Completeness of the response. 
7.	Best response: Obtaining the best response by sorting the evaluation scores, and obtaining the top relevant content for the given query. 

## Environment Setup:

Creating a conda environment or python venv. Implement the following on `terminal/cmd`.
If Conda: 
```
conda create --name adv_rag
conda install pip
pip install -r requirements.txt
```

If Python venv:
```
python3 -m venv .adv_rag
source .venv/bin/activate
python install -r requirements.txt
```

## Code: 
Please go to `AdvRAG_tutorial.ipynb` file in the directory to run the end-to-end Adv RAG Implementation example. 
