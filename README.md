

# Database Chatbot

A conversational AI chatbot that interacts with your Supabase database. It translates natural language queries into SQL commands, executes them, and returns results. It also supports generating visualizations like graphs using Matplotlib, asks clarifying questions when needed, and maintains conversation history for context-aware responses.

## Features

- **Natural Language Queries:** Ask questions like `"Give me clients' names"`, and the chatbot will generate and execute the appropriate SQL query on your Supabase database to fetch and display the results.
- **Graph Generation:** Request visualizations, e.g., `"Give me clients' birthdays per year graph"`. The chatbot generates SQL, runs it, creates Matplotlib code, executes it, and returns the chart.
- **Clarification Questions:** If a query is ambiguous (e.g., `"Give me names"`), the chatbot will ask follow-up questions like `"What table's names?"` to refine the request.
- **Conversation History:** Maintains context across interactions. For example, after `"Give me clients' names"`, a follow-up like `"Give me their emails"` will automatically reference the clients from the previous query.
- **Backend Integration:** Powered by Python with Supabase connectivity for database operations.
- **Frontend Interface:** A web-based chat interface built with modern JavaScript frameworks.

## Installation

```bash
# Clone the repository
git clone https://github.com/Ahmed-Memni/stage-final.git

# Navigate to the backend directory
cd ./Backend

# Create and activate a virtual environment
python -m venv venv
.\venv\Scripts\Activate.ps1

# Install backend dependencies
pip install -r requirements.txt

# Start the backend server
uvicorn src.main:app --host 0.0.0.0 --port 8000

# In a new terminal, navigate to the frontend directory
cd ./Frontend

# Install frontend dependencies
npm install

# Run the frontend development server
npm run dev
```
The application should now be running on your localhost (typically at `http://localhost:5173` for the frontend, connecting to the backend at port `8000`).

### Usage

1. Open the frontend in your browser.
2. On startup, the frontend will prompt you to provide your Supabase connection string.
3. After entering the connection string, the chatbot interface will load.
4. Start chatting with the bot by typing natural language queries related to your database.
5. For graphs, the bot will generate and display Matplotlib-based charts directly in the chat interface.

## Agent Reasoning (Thought Process)

The chatbot doesn't just blindly run queries—it uses an **AgentExecutor chain** to plan its actions step by step. This allows it to generate SQL, run visualizations, handle errors, and give context-aware responses. Here’s how it works:

### Example: Retrieving Client Emails

**User Query:**
`Give me clients' emails`

**Agent Thought Process:**

```
> Entering new AgentExecutor chain...
Thought: I need to retrieve all client emails from the clients table.
Action: sql_query
Action Input: Retrieve all client emails from the clients table.
```

**SQL Generated:**

```sql
SELECT email FROM clients ORDER BY email;
```

**SQL Response:**

```
jean.dupont@example.com
sophie.martin@example.com
jean.lemoine@example.com
...
```

**Agent Final Answer:**

```
Here are the emails:
- jean.dupont@example.com
- sophie.martin@example.com
- jean.lemoine@example.com
...
> Finished chain.
```

---

### Example: Generating a Graph

**User Query:**
`Give me clients' birthdays per year graph`

**Agent Thought Process:**

```
> Entering new AgentExecutor chain...
Thought: I need to count clients' birthdays per year to generate a graph.
Action: graph_query
Action Input: Count clients' birthdays per year to generate a graph.
```

**SQL Generated:**

```sql
SELECT EXTRACT(YEAR FROM "date_naissance") AS "year",
       COUNT(*) AS "count"
FROM clients
GROUP BY EXTRACT(YEAR FROM "date_naissance")
ORDER BY "year";
```

**SQL Result:**

```
   count  year
0      1  1975
1      1  1985
2      1  1988
...
```

**Matplotlib Code Generated:** (internal)

```python
plt.bar(data['year'], data['count'], color='skyblue')
plt.title('Client Birthdays per Year')
plt.xlabel('Year')
plt.ylabel('Count')
plt.savefig('chart.png')
```

**Agent Final Answer:**

```
Here is the chart of "clients' birthdays per year".
> Finished chain.
```
