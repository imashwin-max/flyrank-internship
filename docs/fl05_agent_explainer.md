# Agents vs. Workflows: Upgrading the Search Intelligence Pipeline

As AI capabilities expand, the terminology used to describe them has become increasingly muddled. The word "agent" is frequently misapplied to basic scripts and LLM wrappers. To build reliable systems, we must distinguish between deterministic workflows and autonomous agents, and understand the protocols—like MCP—that allow these models to interact with the outside world.

## 1. Workflows vs. Agents: The Core Distinction
At its core, a **workflow** is a deterministic, pre-defined sequence of events. It relies on hardcoded paths and specific triggers. If a system requires a human to press "go," paste input into a box, and wait for a sequence of chained prompts to execute in a specific order (e.g., Gather -> Draft -> Critique -> Polish), it is a workflow. Workflows are highly predictable and excel at well-defined tasks where the inputs and expected outputs are known.

An **agent**, however, operates with a degree of autonomy. While a workflow follows a rigid path, an agent is given a goal and a set of tools, and it uses an LLM to *decide* the path. An agent routes its own logic, chooses which tool to invoke, evaluates the output of that tool, and determines if it needs to correct course before finally reporting back to the user. If an LLM is actively deciding *how* to solve the problem step-by-step rather than just following a hardcoded script, it is an agent.

## 2. Classifying My FL-04 Pipeline
My FL-04 pipeline—the "Draft, Critique, Revise" Search Intelligence Brief—is strictly a **workflow**. 

While it uses an LLM to synthesize data and critique its own writing, it possesses zero autonomy. I (the human) must find the article, copy the text, paste it into the Claude Project, and manually trigger the prompt chain. The system does not decide when to run, where to fetch data, or how to route the output. It is a highly efficient, chained automation, but it is not an agent.

## 3. What is MCP? (Model Context Protocol)
To transform a trapped LLM into an agent that can interact with the world, it needs secure, standardized access to external systems. This is where **MCP (Model Context Protocol)** comes in. Designed by Anthropic, MCP acts as a "USB-C port for AI applications." It is a standardized, open-source protocol that allows AI models to connect securely to local files, databases, and APIs without requiring custom integrations for every new tool.

MCP relies on three core primitives:
1. **Tools:** These are executable actions the model can trigger. For example, a tool might allow the AI to run a bash command, query a database, or push a message to Slack. The model decides when to invoke the tool and passes the required arguments.
2. **Resources:** These provide context and read-only data. Instead of pasting a 50-page PDF into the chat window, an MCP resource exposes the file structure or database schema so the model can read it on demand.
3. **Prompts:** These are standardized templates and instructions that help the model format requests or structure its outputs when interacting with a specific MCP server.

By standardizing how models talk to data, MCP eliminates the need for brittle, custom-built API connectors.

## 4. Upgrading FL-04 to a True Agent
To upgrade my FL-04 Search Intelligence Brief from a manual workflow to a true autonomous agent, I would need to integrate it with an MCP server and grant the LLM routing autonomy. 

Here is what the upgrade would look like:
*   **MCP Tool - Web Search & RSS Reader:** Instead of me pasting articles, the agent would be given a tool to actively poll an RSS feed of search engine blogs or query a live web search for new algorithmic updates.
*   **MCP Tool - File System Writer:** Instead of generating text in a chat window, the agent would use a file system tool to automatically generate, format, and save the markdown brief into my local `/docs/` folder.
*   **Agentic Routing:** The LLM would be given a goal: *"Check for search engine updates daily. If a major algorithm update is detected, extract the facts, draft a brief, critique it for fluff, and save it to the workspace."* 

The model would use its autonomy to decide *if* an article is worth summarizing, invoke the reading tool to gather the text, run its own internal critique loop, and finally invoke the file-writing tool to save the final output—completely removing the human from the trigger loop.
