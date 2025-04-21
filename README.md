
# HANA AI Assistant 🤖

This project demonstrates a conversational AI assistant built with Streamlit and powered by OpenAI's GPT models. It allows users to interact with an SAP HANA database, generate charts, fetch external data (like weather), execute OS commands

## Architecture Overview

The application uses an LLM (OpenAI GPT-4o) as a central orchestrator. Based on user input and a detailed system prompt:

1.  The **LLM** understands the user's request and plans the necessary steps.
2.  It selects the appropriate **Agent** (a specialized Python function) and generates the required input (e.g., SQL query, chart parameters, city name, command etc).
3.  The **Streamlit App** receives instructions from the LLM (via JSON) and calls the corresponding local Agent function.
4.  The **Agent** executes its task, potentially interacting with **External Services** (SAP HANA Cloud, Weather API, Server OS).
5.  The Agent returns the result to the Streamlit App.
6.  The Streamlit App sends an **Observation** back to the LLM, informing it of the outcome.
7.  The LLM determines the next step or generates the final response for the user.
8.  The **Streamlit App** displays the final answer, data, or chart to the user.

![image](https://github.com/user-attachments/assets/a96c99ad-cf8d-4983-a0ed-396fe3d62567)



## Features

*   **Natural Language Querying:** Interact with HANA data using plain English.
*   **Text-to-SQL:** Automatically generates SQL queries based on user requests.
*   **Data Visualization:** Creates line and bar charts from query results (`create_chart` agent).
*   **External API Integration:** Fetches real-time weather data (`get_weather` agent).
*   **Command Execution:** Runs safe, predefined shell commands (`run_command` agent).
*   **Input Validation:** Basic checks to prevent overly broad/unsafe queries.
*   **Professional UI:** Styled interface using Streamlit.

