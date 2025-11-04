# Multi-Agent Research System with LangGraph

A sophisticated multi-agent AI system powered by LangGraph and Groq that coordinates specialized agents to research topics, analyze data, and generate comprehensive reports.

## 🌟 Features

- **Supervisor-Orchestrated Workflow**: Intelligent supervisor agent that coordinates task delegation
- **Specialized Agent Roles**: Three expert agents working in sequence
  - 🔍 **Researcher**: Gathers comprehensive information and data
  - 📊 **Analyst**: Analyzes research findings and extracts insights
  - ✍️ **Writer**: Creates professional, structured reports
- **Powered by Groq**: Fast inference using Groq's LLaMA 3.1 8B model
- **State Management**: Robust state tracking with LangGraph
- **Sequential Pipeline**: Automatic progression through research → analysis → writing

## 🏗️ Architecture

```
┌─────────────┐
│  Supervisor │ ←─────────┐
└──────┬──────┘           │
       │                  │
       ├─→ 🔍 Researcher ─┤
       │                  │
       ├─→ 📊 Analyst ────┤
       │                  │
       └─→ ✍️ Writer ─────┘
```

### Workflow

1. **Task Entry** → Supervisor receives the task
2. **Research Phase** → Researcher gathers information
3. **Analysis Phase** → Analyst extracts insights and patterns
4. **Writing Phase** → Writer creates final report
5. **Completion** → Supervisor marks task as complete

## 📋 Prerequisites

- Python 3.8+
- Groq API key
- Required packages:
  - `langchain`
  - `langchain-core`
  - `langgraph`
  - `groq`

## 🚀 Installation

1. **Clone or download the project files**

2. **Install dependencies**:
```bash
pip install langchain langchain-core langgraph groq
```

3. **Set up your Groq API key**:
```bash
export GROQ_API_KEY="your-api-key-here"
```

## 💻 Usage

### Basic Example

```python
from langchain_core.messages import HumanMessage

# Initialize the task
task = HumanMessage(content="Research the impact of artificial intelligence on healthcare")

# Run the workflow
result = graph.invoke({
    "messages": [task]
})

# Access the final report
print(result["final_report"])
```

### Advanced Usage

```python
# Stream the execution to see agent progression
for output in graph.stream({"messages": [task]}):
    for key, value in output.items():
        print(f"\n{'='*50}")
        print(f"Agent: {key}")
        print(f"{'='*50}")
        if "messages" in value:
            print(value["messages"][-1].content)
```

## 📁 Code Structure

```
├── SupervisorState          # State management class
├── create_supervisor_chain() # Supervisor decision logic
├── supervisor_agent()       # Orchestrates workflow
├── researcher_agent()       # Gathers information
├── analyst_agent()         # Analyzes data
├── writer_agent()          # Creates reports
├── router()                # Routes between agents
└── graph                   # Compiled workflow
```

## 🔧 How It Works

### 1. Supervisor Agent
- Evaluates current state (what's completed)
- Decides which agent should work next
- Uses LLM to make intelligent routing decisions
- Monitors task completion

### 2. Researcher Agent
Gathers comprehensive information including:
- Key facts and background
- Current trends or developments
- Important statistics or data points
- Notable examples or case studies

### 3. Analyst Agent
Analyzes research data to provide:
- Key insights and patterns
- Strategic implications
- Risks and opportunities
- Actionable recommendations

### 4. Writer Agent
Creates a structured report with:
- Executive Summary
- Key Findings
- Analysis & Insights
- Recommendations
- Conclusion

## ⚙️ Configuration

### Changing the LLM Model

```python
# Use a different Groq model
llm = init_chat_model("groq:llama-3.1-70b-versatile")

# Or use a different provider
llm = init_chat_model("anthropic:claude-3-5-sonnet-20241022")
```

### Customizing Agent Behavior

Modify the prompts in each agent function to customize their behavior:

```python
def researcher_agent(state: SupervisorState) -> Dict:
    research_prompt = f"""Custom instructions here..."""
    # ... rest of the function
```

## 📊 Example Output

```
📋 Supervisor: Let's start with research. Assigning to Researcher...

🔍 Researcher: I've completed the research on 'AI in healthcare'.
Key findings:
[Research summary...]

📋 Supervisor: Research done. Time for analysis. Assigning to Analyst...

📊 Analyst: I've completed the analysis.
Top insights:
[Analysis summary...]

📋 Supervisor: Analysis complete. Let's create the report. Assigning to Writer...

✍️ Writer: Report complete! See below for the full document.

📄 FINAL REPORT
==================================================
Generated: 2025-11-04 14:30
Topic: AI in healthcare
==================================================
[Full report...]
==================================================
```

## 🎯 Use Cases

- **Market Research**: Analyze market trends and generate insights
- **Competitive Analysis**: Research competitors and create strategic reports
- **Technology Evaluation**: Assess new technologies and their implications
- **Business Intelligence**: Gather and analyze business data
- **Academic Research**: Compile research on academic topics

## 🛠️ Troubleshooting

### Common Issues

**Issue**: "Groq API key not found"
- **Solution**: Ensure your `GROQ_API_KEY` environment variable is set

**Issue**: "Agent gets stuck in a loop"
- **Solution**: Check the router logic and ensure `next_agent` is properly set

**Issue**: "LLM returns unexpected format"
- **Solution**: Adjust the supervisor prompt to be more specific about output format

## 🚀 Future Enhancements

- [ ] Add more specialized agents (e.g., fact-checker, editor)
- [ ] Implement parallel agent execution for independent tasks
- [ ] Add memory/checkpoint support for long-running tasks
- [ ] Create a web interface for easier interaction
- [ ] Add support for document uploads and processing
- [ ] Implement human-in-the-loop feedback


---

**Built with** ❤️ **using LangGraph and Groq**
