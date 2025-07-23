🌍 Travel Planner Agentic System using Granite-3-8B-Instruct on watsonx.ai
Technology Stack: IBM watsonx.ai, LangChain, Python, Wikipedia API, Open-Meteo API

Overview

This project demonstrates how to build an intelligent Travel Planner Agent using the Granite-3-8B-Instruct model from IBM watsonx.ai. The agent can:
	•	Retrieve current weather information for a given city.
	•	Suggest top attractions using Wikipedia.
	•	Combine reasoning and real-time tool access to provide personalized trip planning.

Problem Statement

Planning a trip is complex due to factors like weather, places of interest, and logistics. Traditional LLMs struggle with real-time data (e.g., recent closures or current weather).
This project solves that by integrating AI agents with external tools using LangChain.

🧠 What are AI Agents?

AI agents combine:
	•	A Large Language Model (LLM) as a reasoning engine.
	•	A set of external tools to fetch real-time or domain-specific data.
	•	Memory to track previous interactions.

In this project:
	•	LLM: Granite-3-8B-Instruct on watsonx.ai
	•	Tools:
	•	Wikipedia API (for places to visit)
	•	Open-Meteo API (for live weather updates)

 🚀 Features

✅ Uses LangChain to orchestrate agents
✅ Connects to Wikipedia for top attractions
✅ Fetches real-time weather data using Open-Meteo
✅ Supports memory and context tracking
✅ Built with modular architecture using tools and prompt templates

Prerequisites
	•	IBM Cloud account
	•	A project in watsonx.ai
	•	Jupyter Notebook or Python environment
	•	An .env file with:
WATSONX_URL=
WATSONX_APIKEY=
WATSONX_PROJECT_ID=

⚙️ Installation

Install required dependencies:

%pip install git+https://github.com/ibm-granite-community/utils \
    langchain \
    langchain_community \
    ibm_watsonx_ai \
    langchain_ibm \
    wikipedia

Project Structure:
travel-planner-agent/
├── travel_agent.ipynb        # Main Jupyter notebook
├── .env                      # Environment variables
├── README.md                 # This file
└── utils/                    # (Optional) Helper functions or wrappers

Core Components

🔹 1. LLM Setup

Configure WatsonxLLM with:
	•	Decoding method
	•	Stop sequences
	•	Token limits

🔹 2. Tools
	•	WikipediaTool: Scrapes Wikipedia for tourist attractions.
	•	OpenMeteoTool: Fetches current weather from latitude/longitude via Open-Meteo API.

🔹 3. Prompt Engineering

Creates structured system/human prompts to guide the agent’s behavior:
	•	Enforces tool use
	•	Returns structured responses
	•	Enables tool selection reasoning

🔹 4. Agent Memory
Uses ChatMessageHistory to retain prior context.

🔹 5. Agent Execution
Chains prompt, tools, and LLM using LangChain’s AgentExecutor and RunnableWithMessageHistory.

Sample Queries:
# Query 1: Weather in New York
agent_with_chat_history.invoke({
    "input": "How is the weather in New York?"
}, config={"configurable": {"session_id": "watsonx"}})

# Query 2: Full travel recommendation
agent_with_chat_history.invoke({
    "input": "I am planning a trip to New York next week. Can you gather information about the best places to visit, provide a weather forecast, and recommend activities based on current events and conditions?"
}, config={"configurable": {"session_id": "watsonx"}})

Output Example:
Action:
```json Further Resources

{
  "action": "OpenMeteoTool",
  "action_input": "New York"
}

Observation: Current temperature in New York is 27°C, windspeed 4.5 m/s, and it is daytime.

Action:
{
  "action": "WikipediaTool",
  "action_input": "New York City attractions"
}
Observation: Top attractions include Statue of Liberty, Central Park, Times Square, Metropolitan Museum of Art, etc.


 Further Resources
	•	IBM watsonx.ai
	•	LangChain Documentation
	•	Granite Model on HuggingFace
	•	Wikipedia API
	•	Open-Meteo API

📝 License
This project is open-sourced under the MIT License.

    
