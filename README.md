# AGENT → LLM + RAG + Prompt Engineering

This project demonstrates the integration of Large Language Models (LLMs), Retrieval-Augmented Generation (RAG) with agents, and Prompt Engineering using the PromptTemplate class. The goal is to showcase how open-source and proprietary LLMs (like Falcon and GPT-3.5 Turbo) can be used with a retrieval system to generate contextually relevant responses.

## Project Overview

- **LLM Integration**: Utilizes open-source models like Falcon and proprietary models like GPT-3.5 Turbo for text generation.
- **Retrieval-Augmented Generation (RAG)**: Enhances the LLM by retrieving relevant documents from a local dataset using a custom retriever.
- **Prompt Engineering**: Constructs prompts using `PromptTemplate` to guide the LLM's response generation.
- **Agents**: Integrates tools and agents to automate and streamline the process of answering questions based on retrieved context.

## Main Components

- **Custom Retriever**: A custom class around the retriever to limit the number of retrieved documents.
- **Custom Embeddings**: Uses SentenceTransformer to create embeddings for documents and queries.
- **Context Generation**: Retrieves relevant context from a file using the RAG setup.
- **LLMChain**: Manages the pipeline of prompt creation and response generation.
- **Agent**: Combines tools and LLM to provide responses based on retrieved context.

## Usage Example

```python
question = '<Ask question regarding information that can only be found in the resource file>'
context = get_context(question, 'my_file.txt', 1)
template = """
You are a helpful assistant. Use the following context to answer the question very concisely.

Context: {context}

Question: {question}

Answer:
"""
prompt = PromptTemplate(input_variables=["context", "question"], template=template)
llm_chain = LLMChain(llm=llm, prompt=prompt)
response = llm_chain.run({"context": context, "question": question})
print(response)
