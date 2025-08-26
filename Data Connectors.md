### Data Connectors

Data Connectors are modules in LlamaIndex that let you ingest data from different sources (files, databases, APIs, cloud storage, etc.).

Think of them as “bridges” between your external data and LlamaIndex’s internal document representation (Document objects).

They help you load, preprocess, and chunk data so it can later be embedded, indexed, and queried.

**Example** : PDF,CSV,HTML etc..

```python
from llama_index.core import VectorStoreIndex, SimpleDirectoryReader

#Step 1: Use a data connector to load documents from a folder
documents = SimpleDirectoryReader("data/").load_data()

#Step 2: Create an index from the documents
index = VectorStoreIndex.from_documents(documents)

#Step 3: Query the index
query_engine = index.as_query_engine()
response = query_engine.query("What is the summary of this document?")
print(response)
```

**Popular Data Connectors in LlamaIndex**

**Some built-in connectors include:**

**File-based:** SimpleDirectoryReader, PDFReader, DocxReader

**Databases:** DatabaseReader, PandasQueryEngine

**Cloud/Apps:** Notion, Slack, Google Drive, Github

**Web:** BeautifulSoupWebReader, WikipediaReader

**🔹 Types of Loaders in LlamaIndex (with Examples)**

**1. File-based Loaders 📂**

Used for local files like .pdf, .docx, .txt, .csv, etc.

**Example: Directory Loader**

```python
from llama_index.core import SimpleDirectoryReader

#Load all files from "data" folder
documents = SimpleDirectoryReader("data/").load_data()

print(len(documents), "documents loaded")
print(documents[0].text[:200])   # preview first doc text
```

**2. PDF and Docx Loaders 📑**

For directly handling documents.

**Example: PDF Loader**

```python
from llama_index.readers.file import PDFReader

reader = PDFReader()
documents = reader.load_data(file="report.pdf")

print(documents[0].text[:300])
```

**3. Database Loaders 🗄️**

For SQL databases or Pandas DataFrames.

**Example: SQL Database Loader**

```python
from sqlalchemy import create_engine
from llama_index.readers.database import DatabaseReader

engine = create_engine("sqlite:///example.db")

reader = DatabaseReader(engine, include_tables=["users"])
documents = reader.load_data()

print(documents[0].text[:200])
```

**4. Web Loaders 🌐**

For scraping and ingesting from websites.

**Example: Web Page Loader**

from llama_index.readers.web import SimpleWebPageReader

urls = ["https://docs.llamaindex.ai/en/stable/"]
documents = SimpleWebPageReader().load_data(urls)

print(documents[0].metadata)

| **Category** | **Examples**                                           | **Use Cases**                 |
| ------------ | ------------------------------------------------------ | ----------------------------- |
| File-based   | `SimpleDirectoryReader`, `PDFReader`, `DocxReader`     | Local PDFs, Word docs         |
| Database     | `DatabaseReader`, `PandasCSVReader`                    | SQL, CSV, Pandas data         |
| Web          | `SimpleWebPageReader`, `WikipediaReader`               | Websites, Wikipedia           |
| App/Cloud    | `NotionPageReader`, `GoogleDriveReader`, `SlackReader` | SaaS integrations             |
| Custom       | Subclass `BaseReader`                                  | Any data source not supported |




**🔹 What is a Document in LlamaIndex?**

A Document is the basic unit of data in LlamaIndex.

Whenever you load data from a source (PDF, SQL, website, etc.) using a Data Connector, that raw data is converted into a Document object.

Internally, a Document is just text + metadata.

Think of it like this:

📂 File → 📝 Document → (later) 📦 Index

**🔹 What is a Node in LlamaIndex?**

A Node is a smaller chunk of text created by splitting a Document.

Since Documents can be very large (e.g., a 200-page PDF), they are too big for an LLM’s context window.

So, LlamaIndex breaks Documents into Nodes → smaller, manageable text chunks that can be embedded and retrieved efficiently.

👉 Think of it like this:
📂 File → 📝 Document → 📑 Nodes (chunks of text)

