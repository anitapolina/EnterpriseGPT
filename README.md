# EnterpriseGPT
Conversational bot using GPT for enterprise data retrieval.

This repository contains the implementation of an **Enterprise GPT Bot** that enables conversational data retrieval from uploaded documents. The bot is built using Python, LangChain, and OpenAI APIs, and features a user-friendly dashboard for interactive queries.

---

## Features
- **Multi-Document Support:** Load multiple PDFs for querying.
- **Conversational Memory:** Maintains context across multiple queries.
- **Interactive Dashboard:** Built with Panel for seamless interaction.
- **OpenAI Integration:** Utilizes GPT-4 for accurate and context-aware responses.

---

## Installation
### Prerequisites
Ensure you have Python 3.8 or above installed.

### Steps
1. Clone the repository:
   ```bash
   git clone <repository-url>
   cd <repository-name>
   ```
2. Install the required dependencies:
   ```bash
   pip install -r requirements.txt
   ```
3. Set your OpenAI API key as an environment variable:
   ```bash
   export OPENAI_API_KEY='your-api-key'
   ```

---

## Usage
### Running the Bot
1. Start the application by running the script:
   ```bash
   python Enterprise_GPT.py
   ```
2. Open the Panel dashboard in your browser (usually at `http://localhost:5006`).

### Interacting with the Dashboard
- **Upload Documents:** Use the file input widget to upload PDF documents.
- **Ask Questions:** Enter your queries in the text input box.
- **View Results:** The chatbot will provide context-aware responses along with the source documents.

---

## Code Overview
### Key Functions and Classes
1. **Document Loading:**
   - Uses `PyPDFLoader` to load PDF files and `RecursiveCharacterTextSplitter` to split text into chunks for processing.
2. **Vector Database Creation:**
   - Creates a vector database with OpenAI embeddings for similarity-based retrieval.
3. **Conversational Chain:**
   - Implements `ConversationalRetrievalChain` to handle conversational queries.
4. **Dashboard:**
   - Built with Panel to provide an interactive interface for document uploading, querying, and result viewing.

### Main Script Highlights
#### Document Loader
```python
loaders = [PyPDFLoader(file) for file in files]
documents = []
for loader in loaders:
    documents.extend(loader.load())

text_splitter = RecursiveCharacterTextSplitter(chunk_size=1000, chunk_overlap=150)
docs = text_splitter.split_documents(documents)
```
#### Conversational Chain
```python
qa = ConversationalRetrievalChain.from_llm(
    llm=ChatOpenAI(model_name="gpt-4-1106-preview", temperature=0, openai_api_key='Your API Key'),
    chain_type="stuff",
    retriever=retriever,
    return_source_documents=True,
    return_generated_question=True,
)
```
#### Dashboard Setup
```python
pn.extension()
dashboard = pn.Column(
    pn.Row(pn.pane.Markdown('# ChatWithYourData_Bot')),
    pn.Tabs(
        ('Conversation', tab1),
        ('Database', tab2),
        ('Chat History', tab3),
        ('Configure', tab4)
    )
)
dashboard
```

---

## Contributing
Feel free to fork this repository and submit pull requests. For major changes, please open an issue to discuss what you would like to change.

---

## Acknowledgments
- [LangChain](https://langchain.com/) for providing robust tools for document retrieval.
- [Panel](https://panel.holoviz.org/) for the interactive dashboard.
- [OpenAI](https://openai.com/) for GPT-4 and embedding APIs.

Happy coding!

