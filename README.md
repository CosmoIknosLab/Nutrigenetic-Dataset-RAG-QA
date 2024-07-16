# Retrieval-Augmented Generation (RAG) for Question-Answering in the Nutrigenetics Domain

This repository contains the dataset and supplementary materials for our paper titled "A Retrieval-Augmented Generation application for Question-Answering in Nutrigenetics Domain". The main focus is on the creation and utilization of a semantified dataset, employing MeSH ontology for implementing RAG in the domain of nutrigenetics.

## Repository Structure

### Data
The `data` directory contains the processed dataset used for the implementation of the RAG methodology.

- **RAG_LLM_nutrigentic_dataset.zip**: This zip file contains the dataset, semantified with MeSH ontology, used for RAG implementation of LLMs in the nutrigenetics domain.

#### Dataset Overview
Our dataset is meticulously curated and processed to ensure its relevance and accuracy in the nutrigenetic domain. The dataset comprises extracted abstracts from PubMed, annotated with MeSH terms (Medical Subject Headings).

**Sample Data Structure:**

| pubmed_id | title     | abstract | keywords | descriptors |
|-----------|-----------|----------|----------|-------------|
| 34445694  | Mitochondrial Dysfunction in Vascular Wall Cell... | Altered mitochondrial function... | ['atherosclerosis', 'inflammation', 'mitochond... | [{'descriptor': 'Antioxidants', 'qualifier': '...  |

The dataset includes the following fields:
- **pubmed_id**: Unique identifier for PubMed articles.
- **title**: Title of the article.
- **abstract**: Abstract of the article.
- **keywords**: Keywords associated with the article, parsed into lists.
- **descriptors**: MeSH descriptors, including major and minor qualifiers.

**Data Preprocessing**:
- The dataset was built by De Filippis et al., merging human genetic data and literature annotations from LitVar and PubMed.
- Only protein-coding genes were considered.
- We collected 37,042 abstracts associated with specific MeSH terms.


![Workflow](imgs/rag-framework.png, "Diagram showing the RAG Framework")

## Usage
### Loading the Dataset
To load and explore the dataset, first unzip the `RAG_LLM_nutrigentic_dataset.zip` file. The dataset is stored in a CSV format, which can be easily loaded using pandas in Python.

```
df = pd.read_csv('data/RAG_LLM_nutrigentic_dataset.csv')
```


### Applying the RAG Framework
This dataset is designed to be applied for advanced question-answering tasks within the nutrigenetics domain, allowing researchers and professionals to retrieve accurate and up-to-date scientific information efficiently.

The RAG framework aims to enhance Large Language Models (LLMs) by augmenting their input with domain-specific information retrieved from a vector database. By integrating the rich dataset of nutrigenetics abstracts annotated with MeSH terms, the RAG approach significantly improves the relevance and accuracy of the LLMs' responses. Here is a step-by-step guide on how to apply the RAG framework:

#### Components:
1. **Embeddings Model**:
    - Use the General Text Embeddings (GTE) model to transform the source documents into vector representations. The GTE model is chosen for its superior performance in representing the semantic content of documents using multi-stage contrastive learning.
    - Example:
      ```python
      from gte import GTE  # Hypothetical import for GTE
      gte_model = GTE()
      embeddings = gte_model.transform(documents)
        ```

2. **Vector Database (VDB)**:
    - Utilize Milvus for storing and retrieving the vector data. Milvus is selected for its optimized vector search functionality and supports integration via API.
    - Example:
      ```python
      from pymilvus import connections, Collection
      connections.connect(alias="default", host="localhost", port="19530")

      # Create a Milvus collection
      collection = Collection("nutrigenetics_collection")
      collection.load()
      ```

3. **Query Processing**:
   - Process the query from the user by converting it into a vector using the same Embeddings Model. Retrieve relevant documents from the vector database based on this embedding.
   - Example:
     ```python
     query = "What is the role of genetic polymorphisms in oxidative stress?"
     query_vector = gte_model.transform([query])

      # Search the vector database
      search_params = {"metric_type": "L2"}
      results = collection.search(query_vector, "embeddings", search_params)
      ```

4. **LLMs for Response Generation**:
   - Use GPT-3.5 or Mistral-7B to generate responses. Incorporate the retrieved documents' content into the prompt provided to the LLM to enhance the contextual understanding and improve the accuracy of the generated answers.
   - Example:
     ```python
     import openai

      openai.api_key = 'YOUR_API_KEY'  # For GPT-3.5
      prompt = f"{query}\n\nAdditional Context:\n{retrieved_documents_content}"
      response = openai.Completion.create(
      engine="text-davinci-003",  # or other chosen engine
      prompt=prompt,
      max_tokens=150
      )
      print(response.choices[0].text)
      ```

By leveraging the RAG approach, the system can deliver more precise and contextually enriched responses. This methodology serves as an invaluable tool for professionals and consumers seeking reliable information in the rapidly evolving field of nutrigenetics.

# Summary
The RAG framework integrates various technological components to maximize the potential of LLMs in the nutrigenetics domain. By enhancing the models with domain-specific, up-to-date information stored in a vector database, this approach ensures high-quality, accurate, and relevant responses to user queries.
