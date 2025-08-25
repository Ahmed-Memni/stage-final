Got it! Here's a **single, complete README** ready to copy-paste directly into GitHub:

````markdown
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
````

The application should now be running on your localhost (typically at `http://localhost:5173` for the frontend, connecting to the backend at port `8000`).

## Usage

1. Open the frontend in your browser.
2. On startup, the frontend will prompt you to provide your Supabase connection string.
3. After entering the connection string, the chatbot interface will load.
4. Start chatting with the bot by typing natural language queries related to your database.
5. For graphs, the bot will generate and display Matplotlib-based charts directly in the chat interface.

### Example Queries and Responses

**Query:** `Give me clients' emails`
**SQL Generated:**

```sql
SELECT email FROM clients;
```

**Response:**
Here are the emails:

* [jean.dupont@example.com](mailto:jean.dupont@example.com)
* [sophie.martin@example.com](mailto:sophie.martin@example.com)
* [jean.lemoine@example.com](mailto:jean.lemoine@example.com)
* [jean.durand@example.com](mailto:jean.durand@example.com)
* [sophie.moreau@example.com](mailto:sophie.moreau@example.com)
* [sophie.renard@example.com](mailto:sophie.renard@example.com)
* [emma.leroy@example.com](mailto:emma.leroy@example.com)

---

**Query:** `Give me the distribution of total claim amounts by product`
**SQL Generated:**

```sql
SELECT product_name, SUM(total_claim_amount) AS total_claims
FROM claims
GROUP BY product_name;
```

**Response (Graph):**
Chart: Pie chart

*Here is the chart of "total claim amounts by product".*

---

**Query:** `Give me clients' birthdays per year graph`
**SQL Generated:**

```sql
SELECT EXTRACT(YEAR FROM birth_date) AS year, COUNT(*) AS count
FROM clients
GROUP BY year
ORDER BY year;
```

**Response (Graph):**
*Displays a Matplotlib bar chart showing the number of clients born each year.*



