Day 5 – Memory & RAG: An Agent That Remembers and Looks Things Up
Overview
Day 5 focuses on giving an AI agent two new abilities: remembering each customer's conversation independently, and searching the business's documents (policies, FAQs) instead of carrying everything in the prompt. This session explores the three kinds of memory, conversation threads with checkpointers, embeddings, vector databases (ChromaDB), chunking, and Retrieval-Augmented Generation (RAG).

The practical implementation completes the Sweet Crumbs Home Bakery customer-support agent, powered by the Groq API and the GPT-OSS-20B model. By the end of Day 5, the single agent is complete — ready to move to multi-agent systems on Day 6.

Learning Objectives
Understand the three kinds of memory: conversation, customer, and knowledge.

Manage conversations with a checkpointer and a thread_id per customer.

Explain why pasting all documents into a prompt is a bad idea.

Understand embeddings and how meaning becomes numbers.

Store and search documents using ChromaDB, a vector database.

Split long documents into meaningful chunks with overlap.

Build a RAG pipeline: retrieve → augment → generate.

Build a search_faq tool and add it to an agent.

Complete the single-agent sign-off checklist before moving to Level 3.

Topics Covered
1. Three Kinds of Memory
Conversation memory (short-term): messages in the current chat.

Customer memory (long-term): facts saved across chats.

Knowledge: the business's documents and policies.

Choosing the right kind of memory for each piece of information.

2. Conversation Memory with Threads
Using InMemorySaver as a checkpointer.

Creating an agent with checkpointer=InMemorySaver().

Passing config={"configurable": {"thread_id": ...}} with each call.

Keeping separate histories per customer.

Understanding the difference between in-memory and persistent storage.

3. Why Not Put Everything in the Prompt?
Token cost on every call.

Slower responses with long prompts.

The relevant fact gets buried among irrelevant ones.

The principle: search first, send only what's relevant.

4. Embeddings
Text → list of numbers that captures meaning.

Similar meaning → nearby numbers, even with different words.

Why embeddings beat keyword search.

5. Vector Database with ChromaDB
Creating a collection with get_or_create_collection().

Adding documents with .add(ids, documents) or .upsert(...).

Querying with .query(query_texts, n_results).

Understanding results["documents"][0] (list of lists).

6. Chunking
Splitting long documents into pieces with one idea each.

The trade-off between chunk size and precision.

Adding overlap so sentences aren't cut in half.

Natural chunking: one FAQ = one chunk.

7. RAG: Retrieve, Augment, Generate
Retrieve: search the vector database with the customer's question.

Augment: put the top results into the prompt.

Generate: the model answers only from those facts.

Building a search_faq tool with a clear docstring.

The essential rule: "if it isn't there, say you'll check with the owner."

8. Single-Agent Sign-off
Verifying that the complete agent (brain, instructions, tools, memory, knowledge, tests) works.

Testing each kind of customer message.

Confirming the agent is ready for Level 3 (multiple agents).

Practical Implementation
The session includes hands-on exercises such as:

Installing ChromaDB.

Loading 12 bakery facts into a ChromaDB collection.

Testing queries against the collection.

Writing a search_faq tool with a clear docstring.

Creating an agent with InMemorySaver checkpointer.

Running a chat(thread_id, text) function for multiple customers.

Testing that threads keep their own memory.

Adding policy questions to tests.csv.

Running the tests and verifying pass rate.

Testing edge cases (unrelated questions, missing facts).

Technologies & Concepts
Python

Google Colab

LangChain (create_agent, @tool)

LangGraph (InMemorySaver checkpointer)

Groq API

GPT-OSS-20B

ChromaDB (vector database)

Embeddings

RAG (Retrieval-Augmented Generation)

Chunking

Thread-based conversation memory

Exception Handling

Testing and Evaluation
The completed Sweet Crumbs agent was tested with a range of messages covering prices, hours, policies, and conversation memory.

Test Scenario	Expected Behaviour	Result
"Do you deliver? My order is Rs 1,300."	Answers from search_faq: free delivery above Rs 1,000	 Passed
"Does the plum cake have nuts?"	Answers from search_faq: yes, contains nuts	 Passed
"Can I cancel tomorrow morning?"	Answers from search_faq: 12-hour cancellation rule	 Passed
"Do you sell biryani?"	Says it will check with the owner	 Passed
Ravi says "make them eggless" (after 2 plum cakes)	Remembers "them" = plum cakes (same thread)	 Passed
Switch to Sravani's thread	Doesn't remember Ravi's order	 Passed
The agent correctly used search_faq for policy questions, stayed grounded in the retrieved facts, and kept separate memories per customer.

Key Learning Outcomes
By completing Day 5, I gained an understanding of how to:

Explain the three kinds of memory an agent can have.

Use a checkpointer with thread_id for isolated conversations.

Describe why embeddings capture meaning beyond keywords.

Store and search documents with ChromaDB.

Split documents into chunks that hold one idea each.

Build a RAG pipeline where the agent retrieves facts before answering.

Write a search_faq tool with a docstring that lists topics.

Handle "not found" honestly instead of making up answers.

Test an agent across prices, policies, and multi-thread conversations.

Complete the single-agent sign-off checklist.
