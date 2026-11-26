Day 4 – Tools, Structured Output & Google Sheets for AI Agents
Overview
Day 4 focuses on giving an AI agent hands — the ability to fetch live facts and take real actions. This session explores tool use (function calling), writing effective tools with LangChain's @tool decorator, building a tool-using agent with create_agent, handling rate limits and tool errors, generating structured outputs with Pydantic, and saving data to Google Sheets.

The practical implementation extends the Sweet Crumbs Home Bakery customer-support assistant into a full order-taking agent, powered by the Groq API and the GPT-OSS-20B model.

Learning Objectives
Understand why agents need tools beyond text generation.

Explore how function calling (tool use) works under the hood.

Write well-designed tools using @tool with clear names and docstrings.

Build a tool-using agent with create_agent.

Read and debug agent traces.

Handle API rate limits and tool errors gracefully.

Generate structured outputs using Pydantic models.

Save data to Google Sheets using gspread.

Build a complete agent that looks up prices, checks hours, and saves orders.

Topics Covered
1. Why Agents Need Tools
Understanding the limits of an LLM alone.

Using tools for live facts (prices, hours, stock).

Using tools for actions (saving, sending).

Using tools for exact work (maths).

2. How Function Calling Works
Sending tool descriptions along with messages.

Understanding tool calls in the model's reply.

Running tools in your code and returning results as tool messages.

The agent loop: model → tool call → tool result → model.

3. Writing Good Tools with @tool
Using the @tool decorator from langchain.tools.

Naming tools with clear snake_case names.

Adding type hints for every input.

Writing docstrings that explain when to use the tool.

Returning helpful messages on bad input instead of crashing.

4. The Agent with Tools: create_agent
Initializing an agent with a model, tools, and system prompt.

Invoking the agent with a messages list.

Reading the trace to see every step the agent took.

Understanding how model calls and tool calls relate.

5. Rate Limits and Tool Errors
Understanding error 429 (Too Many Requests).

Using max_retries to handle short bursts.

Using try/except around agent calls for polite failures.

Keeping prompts short and testing with small batches.

Using individual API keys per student.

6. Structured Output with Pydantic
Defining record shapes with BaseModel and Field.

Using Literal for restricted values.

Using ge=1 and similar validation rules.

Generating structured outputs with with_structured_output.

Handling validation errors.

7. Saving to Google Sheets
Authenticating with auth.authenticate_user() in Colab.

Authorizing with gspread.authorize(creds).

Creating and opening spreadsheets.

Appending rows with ws.append_row([...]).

8. Putting It Together: log_order
Wrapping check + total + save in one tool.

Using Pydantic inside the tool as a second check.

Making the docstring specify when the tool is ready to use.

Practical Implementation
The session includes hands-on exercises such as:

Installing LangChain, langchain-groq, and gspread.

Connecting the Groq API to Google Colab.

Initializing the GPT-OSS-20B language model with retries.

Authenticating and creating a "Sweet Crumbs Orders" spreadsheet.

Writing a Pydantic Order model with type hints and validation.

Creating tools: get_price, is_open, and log_order.

Building an agent with create_agent and a bakery system prompt.

Chatting with the agent and verifying responses.

Reading the trace with pretty_print().

Testing edge cases (unknown items, missing details, zero quantity).

Verifying that orders are saved correctly to Google Sheets.

Technologies & Concepts
Python

Google Colab

LangChain (@tool, create_agent)

Groq API

GPT-OSS-20B

Pydantic (BaseModel, Field, Literal)

with_structured_output

Google Sheets API (gspread)

Function Calling / Tool Use

Agent Traces

Rate Limits (429)

Exception Handling

Conversation History

Testing and Evaluation
The Sweet Crumbs Home Bakery agent was tested with a range of customer messages covering pricing, opening hours, and order placement.

Test Scenario	Expected Behaviour	Result
Ask Sunday hours + price of 2 chocolate cakes	Correct hours and Rs 1,300 total	✅ Passed
Order 2 eggless chocolate cakes for 24 Dec	Order saved with correct total	✅ Passed
Ask for a "donut" (not on menu)	Agent explains it's unavailable	✅ Passed
Order without giving a date	Agent asks for the missing date	✅ Passed
Order 0 cupcakes	Agent asks the customer to correct	✅ Passed
The agent correctly used tools for prices and timings, saved complete orders to the sheet, and never guessed prices or hours.

Key Learning Outcomes
By completing Day 4, I gained an understanding of how to:

Explain why agents need tools for live facts, actions, and exact work.

Describe how function calling works end to end.

Write well-designed LangChain tools with names, types, and docstrings.

Build a tool-using agent with create_agent.

Read agent traces to debug behaviour.

Handle rate limits and tool errors gracefully.

Define structured records with Pydantic and validate model output.

Save data to Google Sheets using gspread.

Build a complete agent that takes orders from chat to spreadsheet.

Test edge cases and design tools that protect the business's data.
