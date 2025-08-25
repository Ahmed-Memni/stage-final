Database Chatbot
A conversational AI chatbot that interacts with your Supabase database. It translates natural language queries into SQL commands, executes them, and returns results. It also supports generating visualizations like graphs using Matplotlib, asks clarifying questions when needed, and maintains conversation history for context-aware responses.
Features

Natural Language Queries: Ask questions like "Give me clients' names," and the chatbot will generate and execute the appropriate SQL query on your Supabase database to fetch and display the results.
Graph Generation: Request visualizations, e.g., "Give me clients' birthdays per year graph." The chatbot generates SQL, runs it, creates Matplotlib code, executes it, and returns the chart.
Clarification Questions: If a query is ambiguous (e.g., "Give me names"), the chatbot will ask follow-up questions like "What table's names?" to refine the request.
Conversation History: Maintains context across interactions. For example, after "Give me clients' names," a follow-up like "Give me their emails" will automatically reference the clients from the previous query.
Backend Integration: Powered by Python with Supabase connectivity for database operations.
Frontend Interface: A web-based chat interface built with modern JavaScript frameworks.

Installation

Clone the repository:
git clone https://github.com/Ahmed-Memni/stage-final.git


Navigate to the backend directory:
cd ./Backend


Create and activate a virtual environment:
python -m venv venv
.\venv\Scripts\Activate.ps1  


Install backend dependencies:
pip install -r requirements.txt


Start the backend server:
uvicorn src.main:app --host 0.0.0.0 --port 8000


In a new terminal, navigate to the frontend directory:
cd ./Frontend


Install frontend dependencies:
npm install


Run the frontend development server:
npm run dev



The application should now be running on your localhost (typically at http://localhost:5173 or similar for the frontend, connecting to the backend at port 8000).
Usage

Open the frontend in your browser.
On startup, the frontend will prompt you to provide your Supabase connection string.
After entering the connection string, the chatbot interface will load.
Start chatting with the bot by typing natural language queries related to your database.
For graphs, the bot will generate and display Matplotlib-based charts directly in the chat interface.
