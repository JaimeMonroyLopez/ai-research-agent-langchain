# Research Agent with Memory and JSON Output (LangChain)

An AI assistant that **searches Wikipedia**, **summarizes blog posts**, **does math**, **remembers the conversation**, and returns its answers as **JSON**.

## What does it do?

```
"Tell me about the Himalayas"                  →  Wikipedia Search
"Summarize the blog post about remote work"    →  Blog Summarizer
"The peak of the range we discussed is 8,849 m.
 How many feet is that?"                       →  Memory + Calculator  →  29,032 ft
"What topics have we discussed?"               →  Memory only
```

Each answer also comes out as JSON:

```json
{
  "answer": "Mount Everest is approximately 29,032.15 feet tall.",
  "topic": "Mount Everest height",
  "follow_up_question": "What is the prominence of Mount Everest?",
  "tools_used": ["Calculator"]
}
```

## How does it work?

1. The user types a question in a **chat loop**.
2. The agent reads its **system prompt** (its rules) and the **memory** (previous messages).
3. It picks a **tool**: Wikipedia, Blog Summarizer or Calculator.
4. It answers using the tool's real result.
5. A second step turns that answer into **JSON**.

## Key concepts

| Concept | In simple words |
|---|---|
| **System prompt** | The agent's job description: who it is and which tool to use when. |
| **Memory** | Saves every message, so "the range we discussed" means the Himalayas. |
| **Prompt chaining** | Using several prompts in a row: one reasons, one summarizes, one creates JSON. |
| **Structured output** | Answers with fixed fields (JSON), so another program can use them. |
| **Interactive loop** | `chat_loop()` keeps asking questions until you type `exit`. |

## How to run it

```bash
pip install -r requirements.txt
set GOOGLE_API_KEY=your-key        # free key: https://aistudio.google.com/apikey
jupyter notebook research_agent.ipynb
```

To chat live, run `chat_loop()` in a new cell.

## Files

- `research_agent.ipynb`: the agent, with real outputs
- `research_agent.html`: the same notebook, viewable in a browser

## What I learned

- **Memory format matters.** Memory that stores messages needs the *chat* version of the agent.
- **Free APIs have limits.** Gemini's free tier allows 5 requests per minute, so I added a rate limiter.
- **Splitting the work into small prompts** makes each one simpler and more reliable.
- **JSON output** turns a chatbot into something an app can use.
