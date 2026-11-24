README · MD


# Kerala Schemes Assistant
 
A retrieval-augmented generation (RAG) assistant that answers questions about Kerala government schemes, such as "Am I eligible for this scheme?" or "Which documents do I need to apply?", using official scheme documents. Every answer cites the document and page it came from. If the documents do not contain the answer, the assistant says so instead of guessing.
 
Built as my **Month 1 project** for the TinkerHub Maker Fellowship.
 
> **Status: in progress.** This README will be updated as the project develops.
 
> **Disclaimer:** This is a learning prototype, not official advice. Scheme rules change, so always confirm eligibility and procedures with the relevant government department using the linked source documents.
 
## Why this project
 
Scheme information is spread across long PDFs and notifications that are hard to search. People often cannot tell whether they are eligible or what to submit. A question-answering system that shows its sources makes the information easier to reach and easier to verify.
 
## How it works
 
1. **Collect** official scheme documents (PDFs) from Kerala government sources and record each document's source URL and date.
2. **Extract** text page by page, keeping the page number with every piece of text.
3. **Chunk** the text into overlapping passages.
4. **Embed** each chunk with an open embedding model and store the vectors in a vector database.
5. **Retrieve** the most relevant chunks for a user's question.
6. **Generate** an answer with a language model, instructed to use only the retrieved passages, cite them, and say "not found" when the answer is not there.
## Planned tech stack
 
- Python
- PyMuPDF / pypdf for PDF text extraction
- sentence-transformers for embeddings
- Chroma or FAISS for vector search
- An LLM (free API tier or a small local model, to be decided)
- Streamlit or Gradio for the user interface
## Planned features
 
- [ ] Document collection with source tracking (URL and date)
- [ ] Page-level text extraction
- [ ] Chunking and embedding pipeline
- [ ] Retrieval with cited answers
- [ ] "Not found" behaviour for questions the documents do not cover
- [ ] Evaluation set with measured results
- [ ] Simple web interface
- [ ] Stretch: Malayalam documents and questions
## Evaluation
 
To measure quality instead of just demoing, I am building a test set of 30-50 questions with known answers and source pages, including some questions the documents do not answer. I will measure:
 
- **Retrieval accuracy:** is the correct page among the retrieved results?
- **Answer correctness:** is the generated answer right?
- **Citation correctness:** does the cited page actually support the answer?
- **Refusal behaviour:** does it say "not found" when it should?
Then I will change one setting at a time (chunk size, number of retrieved passages, embedding model) and record the effect.
 
| Configuration | Retrieval hit rate | Answer accuracy | Correct citations | Correct "not found" |
|---|---|---|---|---|
| Baseline | TBD | TBD | TBD | TBD |
 
## Project structure
 
```
data/          Source PDFs and a sources list (URL, date)
src/           Extraction, chunking, embedding, retrieval and answering code
eval/          Evaluation questions and scripts
app/           User interface
README.md
```
 
This layout may change as the project develops.
 
## Setup
 
Instructions will be added once the first working version is ready.
 
API keys, if needed, will be read from environment variables and will never be committed to this repository.
 
## Data sources
 
All documents come from official Kerala government publications. A full list with URLs and download dates is kept in `data/sources` (to be added).
 
## What I'm learning
 
- How embeddings and vector search work
- How chunking choices affect retrieval quality
- How to evaluate a RAG system instead of judging it by eye
- How to make answers verifiable with citations
