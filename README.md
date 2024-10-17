# Unstructured Data Extraction Using NLP

## Project Description
This project demonstrates how to extract key entities from unstructured text data using Natural Language Processing (NLP) techniques. It utilizes the spaCy library to identify and classify entities in documents such as company names, locations, and other relevant information. The extracted entities are then organized and saved in a structured format, such as CSV, for further analysis.

## Getting Started

### Prerequisites
Make sure you have Python installed on your system. You will also need to install the following libraries:

- `spaCy`
- `pandas`

### Setup the Environment

```bash
!pip install spacy pandas
!python -m spacy download en_core_web_sm
```

### Load the Data

```python
import pandas as pd

# Mock dataset
data = {
    "documents": [
        "Apple Inc. is based in Cupertino, California and was founded by Steve Jobs.",
        "Tesla, headquartered in Palo Alto, is known for its electric cars.",
        "Microsoft, founded by Bill Gates, is a technology company in Redmond."
    ]
}

df = pd.DataFrame(data)
print(df)
```

### Load the Model

```python
import spacy
nlp = spacy.load('en_core_web_sm')
```

### Process with NLP

```python
# Extract entities from a document
def extract_entities(doc):
    entities = [(ent.text, ent.label_) for ent in doc.ents]
    return entities

# Apply the model
df['entities'] = df['documents'].apply(lambda x: extract_entities(nlp(x)))
print(df[['documents', 'entities']])
```

### Organize and Structure the Data

```python
structured_data = []

for doc, entities in zip(df['documents'], df['entities']):
    for entity, label in entities:
        structured_data.append({'Document': doc, 'Entity': entity, 'Label': label})

structured_df = pd.DataFrame(structured_data)
print(structured_df)

structured_df.to_csv('extracted_entities.csv', index=False)
```

## Usage
1. Clone the repository:
   ```bash
   git clone https://github.com/clizar5302/NLP-Data-Extraction-ColeLizar.git
   cd NLP-Data-Extraction-ColeLizar
   ```

2. Open the Jupyter Notebook:
   ```bash
   jupyter notebook unstructuredDataExtractionNLP.ipynb
   ```

3. Run the cells in the notebook to execute the code and extract entities from the documents.

## License
This project is licensed under the MIT License.

## Acknowledgments
- [spaCy Documentation](https://spacy.io/usage) for the NLP library.
- The dataset used in this project is mock data for demonstration purposes.
