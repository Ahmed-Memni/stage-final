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
