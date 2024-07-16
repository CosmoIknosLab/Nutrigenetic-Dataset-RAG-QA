# A Dataset for Retrieval-Augmented Generation (RAG) for Question-Answering in the Nutrigenetics Domain


This repository contains the dataset and supplementary materials for our paper titled "A Retrieval-Augmented Generation application for Question-Answering in Nutrigenetics Domain". The main focus is on the creation and utilization of a semantified dataset, employing MeSH ontology for implementing RAG in the domain of nutrigenetics.

## Repository Structure

### Data
The `data` directory contains the processed dataset used for the implementation of the RAG methodology.

- `RAG_LLM_nutrigentic_dataset.zip`: This zip file contains the dataset, semantified with MeSH ontology, used for RAG implementation of LLMs in the nutrigenetics domain.

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


## Usage
### Loading the Dataset
To load and explore the dataset, first unzip the `RAG_LLM_nutrigentic_dataset.zip` file. The dataset is stored in a CSV format, which can be easily loaded using pandas in Python.

```
df = pd.read_csv('data/RAG_LLM_nutrigentic_dataset.csv')
```


### Applying the RAG Framework
This dataset is designed to be applied for advanced question-answering tasks within the nutrigenetics domain, allowing researchers and professionals to retrieve accurate and up-to-date scientific information efficiently.

The RAG framework aims to enhance Large Language Models (LLMs) by augmenting their input with domain-specific information retrieved from a vector database. By integrating the rich dataset of nutrigenetics abstracts annotated with MeSH terms, the RAG approach significantly improves the relevance and accuracy of the LLMs' responses. Here is a step-by-step guide on how to apply the RAG framework.


#### Components:
- **Embeddings Model**: Used General Text Embeddings (GTE) for transforming source documents into vector representations.
- **Vector Database (VDB)**: Utilized Milvus for optimal storage and retrieval of vector data.
- **LLMs**: Explored GPT-3.5 and Mistral-7B for generating responses.