# AI Assistant with Model Context Protocol (MCP) Integration

[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![LangChain](https://img.shields.io/badge/LangChain-🦜⛓️-brightgreen)](https://langchain.com/)
[![Groq](https://img.shields.io/badge/Groq-⚡-orange)](https://groq.com/)
[![MCP](https://img.shields.io/badge/MCP-Model_Context_Protocol-purple)](https://modelcontextprotocol.io/)

A sophisticated AI assistant that leverages **Model Context Protocol (MCP)** to seamlessly integrate multiple external services through a unified interface. Built with LangChain and Groq, this project demonstrates cutting-edge AI orchestration capabilities for enterprise applications.

## 🌟 Key Features

- **🔗 Multi-Service Integration**: Connect to browser automation, hotel search, and web search services
- **🤖 Intelligent Agent Framework**: Autonomous tool selection and execution
- **💬 Conversational Memory**: Built-in conversation history and context retention  
- **⚙️ Configuration-Driven**: JSON-based service definitions for easy extensibility
- **⚡ Real-Time Processing**: Asynchronous execution with WebSocket support
- **🏗️ Enterprise-Ready**: Modular architecture for production deployments

## 🚀 What is Model Context Protocol (MCP)?

Model Context Protocol is a revolutionary standard developed by Anthropic that enables Large Language Models to securely connect with external data sources and tools. Instead of building custom integrations for each service, MCP provides:

- **Unified Interface**: One protocol to connect multiple services
- **Service Provider Management**: External services handle their own updates
- **Secure Communication**: Standardized authentication and data exchange
- **Scalable Architecture**: Easy addition of new services without code changes

### Component Breakdown:

1. **MCP Host**: Your development environment (Cursor IDE, VS Code, etc.)
2. **MCP Client**: This application using MCP-Use library
3. **MCP Servers**: External services providing specific capabilities
4. **LLM Integration**: Groq-powered language model for intelligent responses

## 📋 Prerequisites

### Required Software:
- **Python 3.8+** - Programming language runtime
- **Node.js 18+** - Required for npm-based MCP servers
- **UV Package Manager** - Fast Python package manager (recommended)

### API Keys:
- **Groq API Key** - For LLM integration ([Get here](https://console.groq.com/))

### Development Environment:
- **Cursor IDE** (recommended) - AI-powered code editor with MCP support
- **VS Code** (alternative) - Can be configured for MCP integration

## 🛠️ Installation

### 1. Clone the Repository
```bash
git clone https://github.com/Anuj1308/AI-Assistant-with-Model-Context-Protocol-.git
cd mcp-ai-assistant
```

### 2. Set Up Python Environment
```bash
# Using UV (recommended)
uv init mcp-demo
cd mcp-demo
uv venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate

# Or using standard Python
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
```

### 3. Install Dependencies
```bash
# Using UV
uv add langchain-groq
uv add mcp-use
uv add python-dotenv

# Or using pip
pip install langchain-groq mcp-use python-dotenv
```

### 4. Configure Environment Variables
Create a `.env` file in the project root:
```env
GROQ_API_KEY=your_groq_api_key_here
```

### 5. Set Up MCP Server Configuration
Create `browser_mcp.json` in the project root:
```json
{
  "mcpServers": {
    "playwright": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-playwright"]
    },
    "airbnb": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-airbnb"]
    },
    "duckduckgo": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-duckduckgo-search"]
    }
  }
}
```

## 🚀 Usage

### Running the Application

1. **Start the AI Assistant**:
```bash
uv run app.py
# Or: python app.py
```

2. **Interact with the Assistant**:
   - Type your queries in the terminal
   - The assistant will automatically select appropriate tools
   - Exit with `quit` or `Ctrl+C`

### Example Interactions

```bash
# Browser Automation
User: "Please open google.com and then navigate to github.com"
Assistant: I'll help you navigate to these websites using browser automation...

# Hotel Search
User: "Find hotels in Tokyo for April 20th"  
Assistant: I'll search for hotels in Tokyo using Airbnb integration...

# Web Search
User: "What are the latest AI news?"
Assistant: Let me search for the latest AI news using DuckDuckGo...
```

### Cursor IDE Integration

1. **Open Cursor Settings**: `File > Preferences > Cursor Settings`
2. **Navigate to MCP**: Click on "MCP" in the left sidebar
3. **Edit Configuration**: Replace the default configuration with your `browser_mcp.json` content
4. **Restart Cursor**: Close and reopen Cursor to apply changes
5. **Use Agent Panel**: Access the AI agent panel on the right side of Cursor

## 🔧 Configuration

### Adding New MCP Servers

1. **Find MCP Servers**: Browse available servers at [MCP Servers Directory](https://github.com/modelcontextprotocol)

2. **Update Configuration**: Add to `browser_mcp.json`:
```json
{
  "mcpServers": {
    "existing-server": { ... },
    "new-server": {
      "command": "npx",
      "args": ["-y", "@modelcontextprotocol/server-new-service"]
    }
  }
}
```

3. **Restart Application**: The new server will be automatically detected

## 🔍 Available MCP Servers

### Browser Automation (Playwright)
- **Purpose**: Web browser automation and interaction
- **Capabilities**: Page navigation, element interaction, screenshots
- **Use Cases**: Web scraping, UI testing, automated browsing

### Hotel Search (Airbnb)
- **Purpose**: Hotel and accommodation search
- **Capabilities**: Location-based search, availability checking, price comparison
- **Use Cases**: Travel planning, accommodation booking, market research

### Web Search (DuckDuckGo)
- **Purpose**: Internet search functionality
- **Capabilities**: Web search, news aggregation, information retrieval
- **Use Cases**: Research, news updates, general information queries

### Additional Servers (Extensible)
- **GitHub Integration**: Repository management and code analysis
- **Email Services**: Email sending and management
- **Database Connectors**: SQL and NoSQL database interactions
- **File Operations**: Local and cloud file management
- **API Integrations**: Custom REST API connections

## 🐛 Troubleshooting

### Common Issues

#### 1. Node.js Not Found
```bash
# Install Node.js
curl -fsSL https://nodejs.org/dist/v20.9.0/node-v20.9.0-linux-x64.tar.xz | tar -xJ
export PATH=$PWD/node-v20.9.0-linux-x64/bin:$PATH
```

#### 2. MCP Server Connection Errors
```bash
# Test individual servers
npx -y @modelcontextprotocol/server-playwright
npx -y @modelcontextprotocol/server-airbnb
```

#### 3. API Rate Limiting
```python
# Add rate limiting to your requests
import time
time.sleep(1)  # Add delays between API calls
```

#### 4. Memory Issues
```python
# Clear conversation history periodically
if len(conversation_history) > 50:
    conversation_history = conversation_history[-20:]  # Keep last 20 messages
```

### Debug Mode

Enable detailed logging:
```python
import logging
logging.basicConfig(level=logging.DEBUG)

# Or set environment variable
export LANGCHAIN_VERBOSE=true
```

## 🚀 Advanced Usage

### Custom Agent Creation

```python
from mcp_use import create_mcp_agent, MCPClient
from langchain_groq import ChatGroq

# Custom agent with specific capabilities
def create_specialized_agent(task_type):
    if task_type == "research":
        servers = ["duckduckgo", "github"]
    elif task_type == "booking":  
        servers = ["airbnb", "flights"]
    elif task_type == "automation":
        servers = ["playwright", "selenium"]
    
    client = MCPClient(config_file=f"{task_type}_mcp.json")
    return create_mcp_agent(llm=ChatGroq(), client=client)
```

### Streaming Responses

```python
async def stream_chat():
    agent = create_mcp_agent(llm=llm, client=client, streaming=True)
    
    async for chunk in agent.astream({"input": "Search for AI news"}):
        if "output" in chunk:
            print(chunk["output"], end="", flush=True)
```

### Multi-Agent Coordination

```python
# Create specialized agents for different tasks
research_agent = create_specialized_agent("research")
booking_agent = create_specialized_agent("booking")  
automation_agent = create_specialized_agent("automation")

# Coordinate between agents
def coordinate_agents(user_request):
    if "search" in user_request.lower():
        return research_agent.run(user_request)
    elif "book" in user_request.lower():
        return booking_agent.run(user_request)
    elif "automate" in user_request.lower():
        return automation_agent.run(user_request)
```

## 🧪 Testing

### Unit Tests
```bash
# Run tests
python -m pytest tests/

# Test specific component
python -m pytest tests/test_mcp_client.py -v
```

### Integration Tests
```bash
# Test MCP server connectivity  
python tests/test_server_integration.py

# Test end-to-end workflows
python tests/test_e2e_scenarios.py
```

### Manual Testing Scenarios

1. **Browser Automation Test**:
   - Input: "Open YouTube and search for 'AI tutorials'"
   - Expected: Browser opens, navigates to YouTube, performs search

2. **Hotel Search Test**:
   - Input: "Find hotels in Paris for next weekend"
   - Expected: Returns list of available accommodations with details

3. **Web Search Test**:
   - Input: "Latest developments in quantum computing"
   - Expected: Returns recent news articles and research updates

## 🏆 Use Cases & Applications

### Business Applications
- **Customer Support**: Automated ticket resolution with multi-service integration
- **Research & Analysis**: Automated data gathering from multiple sources
- **Travel Planning**: Comprehensive trip planning with real-time availability
- **Content Creation**: Research-backed content generation with fact-checking

### Educational Applications  
- **Interactive Tutoring**: Multi-modal learning with browser-based demonstrations
- **Research Assistance**: Academic paper research with citation management
- **Programming Help**: Code examples with live browser testing

### Personal Productivity
- **Task Automation**: Browser automation for repetitive tasks
- **Information Aggregation**: News and update compilation
- **Travel Management**: Hotel and flight booking assistance
