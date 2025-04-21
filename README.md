
# HANA AI Assistant 🤖

This project demonstrates a conversational AI assistant built with Streamlit and powered by OpenAI's GPT models. It allows users to interact with an SAP HANA database, generate charts, fetch external data (like weather), execute OS commands

## Architecture Overview

The application uses an LLM (OpenAI GPT-4o) as a central orchestrator. Based on user input and a detailed system prompt:

1.  The **LLM** understands the user's request and plans the necessary steps.
2.  It selects the appropriate **Agent** (a specialized Python function) and generates the required input (e.g., SQL query, chart parameters, city name, command, forecast parameters, update filters/note).
3.  The **Streamlit App** receives instructions from the LLM (via JSON) and calls the corresponding local Agent function.
4.  The **Agent** executes its task, potentially interacting with **External Services** (SAP HANA Cloud, Weather API, Server OS).
5.  The Agent returns the result to the Streamlit App.
6.  The Streamlit App sends an **Observation** back to the LLM, informing it of the outcome.
7.  The LLM determines the next step or generates the final response for the user.
8.  The **Streamlit App** displays the final answer, data, or chart to the user.

*(Consider embedding your architecture diagram image here if you have it hosted)*

## Features

*   **Natural Language Querying:** Interact with HANA data using plain English.
*   **Text-to-SQL:** Automatically generates SQL queries based on user requests.
*   **Data Visualization:** Creates line and bar charts from query results (`create_chart` agent).
*   **External API Integration:** Fetches real-time weather data (`get_weather` agent).
*   **Command Execution:** Runs safe, predefined shell commands (`run_command` agent).
*   **Time Series Forecasting:** Generates basic sales forecasts (`perform_forecast` agent).
*   **Data Update:** Adds notes to specific sales records (`update_sales_note` agent - requires DB schema change).
*   **Input Validation:** Basic checks to prevent overly broad/unsafe queries.
*   **Professional UI:** Styled interface using Streamlit and custom CSS, including agent cards and status indicators.

## Setup & Installation

1.  **Clone the repository:**
    ```bash
    git clone https://github.com/<Your-GitHub-Username>/<Your-Repo-Name>.git
    cd <Your-Repo-Name>
    ```
2.  **Create a Virtual Environment (Recommended):**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```
3.  **Install Dependencies:**
    ```bash
    pip install -r requirements.txt
    ```
4.  **Set Up Credentials (IMPORTANT):**
    This application requires credentials for SAP HANA and OpenAI. **Do not hardcode them in `app.py` for production!** Use environment variables:
    *   `OPENAI_API_KEY`: Your OpenAI API key.
    *   `HANA_ADDRESS`: Your HANA Cloud host address.
    *   `HANA_PORT`: Your HANA Cloud port (e.g., 443).
    *   `HANA_USER`: Your HANA database username.
    *   `HANA_PASSWORD`: Your HANA database password.

    You can set these in your terminal before running:
    ```bash
    export OPENAI_API_KEY="sk-..."
    export HANA_ADDRESS="..."
    export HANA_PORT="..."
    export HANA_USER="..."
    export HANA_PASSWORD="..."
    ```
    Alternatively, use a `.env` file (make sure `.env` is in your `.gitignore`!) and a library like `python-dotenv` to load them within `app.py`. Modify the credential loading section in `app.py` accordingly.

5.  **Database Schema (for Update Agent):**
    *   The `update_sales_note` agent requires a `Notes` column (e.g., `NVARCHAR(1000) NULL`) to be added to the `CHOCOLATE_SALES` table in your HANA database. Run the necessary `ALTER TABLE` command if you intend to use this feature.

## Running the App

1.  Ensure your environment variables for credentials are set.
2.  Navigate to the repository directory in your terminal.
3.  Run the Streamlit app:
    ```bash
    streamlit run app.py
    ```
4.  The app should open in your web browser.

## Usage

*   Enter your queries related to the `CHOCOLATE_SALES` data, weather, or simple commands in the text area.
*   Use the example buttons for quick tests.
*   View the results, including data tables, charts, and metrics.
*   Expand the "Show Execution Details" section to see the AI's plan, generated SQL (if any), and agent activation messages.
*   Use the download button to get query/forecast results as a CSV.
