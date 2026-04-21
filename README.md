# LGraph Project

A project demonstrating the implementation of AI agents using LangGraph, featuring both a RAG (Retrieval-Augmented Generation) agent and a ReAct (Reasoning + Acting) agent.

## Project Structure

```
├── RAG_Agent.py         # RAG agent for answering stock market questions
├── ReAct.py             # ReAct agent for arithmetic tasks
├── Stock_Market_Performance_2024.pdf  # Data source for RAG agent
└── README.md            # This documentation
```

## Project Overview

This project showcases two different types of AI agents built with LangGraph:

1. **RAG Agent**: A Retrieval-Augmented Generation agent that answers questions about stock market performance using data from a PDF document.
2. **ReAct Agent**: A Reasoning + Acting agent that performs arithmetic operations through tool use.

## Architecture Design

### 1. RAG Agent Architecture

The RAG agent follows this workflow:

1. **Document Processing**: 
   - Loads and processes the `Stock_Market_Performance_2024.pdf` file
   - Splits the document into chunks for efficient retrieval
   - Creates vector embeddings using DashScope Embeddings
   - Stores embeddings in ChromaDB vector store

2. **Agent Workflow**: 
   - User inputs a question about stock market performance
   - LLM (Qwen 3.6 Plus) generates a response
   - If tool use is needed, the retriever tool searches the vector store
   - Retrieved information is passed back to the LLM
   - LLM generates a final answer based on the retrieved information

3. **Components**: 
   - `call_llm`: Node for invoking the language model
   - `take_action`: Node for executing tool calls
   - `should_continue`: Conditional edge for determining workflow path

### 2. ReAct Agent Architecture

The ReAct agent follows this workflow:

1. **Tool Definition**: 
   - Defines arithmetic tools (add, subtract, multiply)
   - Binds tools to the LLM

2. **Agent Workflow**: 
   - User inputs a query requiring arithmetic operations
   - LLM analyzes the query and determines which tools to use
   - Tool node executes the requested operations
   - Results are passed back to the LLM
   - LLM generates a final answer

3. **Components**: 
   - `model_call`: Node for invoking the language model
   - `ToolNode`: Prebuilt node for executing tool calls
   - `should_continue`: Conditional edge for determining workflow path

## Technology Stack

- **LangGraph**: For building agent workflows and state management
- **LangChain**: For LLM integration and tool management
- **ChromaDB**: For vector storage and retrieval
- **DashScope**: For LLM access (Qwen 3.6 Plus) and embeddings
- **Python 3.10+**: Core programming language

## Getting Started

### Prerequisites

- Python 3.10 or higher
- DashScope API key (for LLM access)

### Installation

1. **Clone the repository**
   ```bash
   git clone <repository-url>
   cd lgraph
   ```

2. **Install dependencies**
   ```bash
   pip install -r requirements.txt
   ```

3. **Set up environment variables**
   Create a `.env` file in the project root with the following content:
   ```
   DASHSCOPE_API_KEY=your_api_key_here
   ```

### Running the Agents

#### RAG Agent

The RAG agent allows you to ask questions about the stock market performance data in the PDF document.

```bash
python RAG_Agent.py
```

Once running, you can ask questions like:
- "What was the performance of tech stocks in 2024?"
- "Which sectors showed the highest growth?"
- "What were the market trends in Q3 2024?"

Type `exit` or `quit` to stop the agent.

#### ReAct Agent

The ReAct agent demonstrates tool use for arithmetic operations.

```bash
python ReAct.py
```

The agent will process a sample query that involves addition and multiplication, then provide the result along with a joke.

## Customization

### RAG Agent

- **Document Source**: Replace `Stock_Market_Performance_2024.pdf` with your own PDF document
- **Chunk Size**: Modify the `chunk_size` and `chunk_overlap` parameters in the `RecursiveCharacterTextSplitter`
- **Search Parameters**: Adjust the `k` value in the retriever to change the number of chunks retrieved
- **LLM Model**: Change the `model` parameter in the `ChatOpenAI` initialization

### ReAct Agent

- **Tools**: Add or modify tools in the `tools` list
- **System Prompt**: Update the system prompt in the `model_call` function
- **Sample Query**: Change the input query in the `inputs` variable

## Project Goals

This project aims to:
1. Demonstrate the implementation of RAG agents for information retrieval
2. Showcase the ReAct pattern for tool-based reasoning
3. Provide a practical example of LangGraph usage for building agent workflows
4. Serve as a starting point for more complex agent-based applications

## Future Enhancements

- Add more tools to the ReAct agent
- Implement memory for conversation context
- Add support for multiple document types in the RAG agent
- Create a web interface for easier interaction
- Add evaluation metrics for agent performance

## License

[MIT License](LICENSE)
