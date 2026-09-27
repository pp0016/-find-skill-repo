# Universal OpenCLI & Agent-Reach Setup Prompt

**Copy/Paste this into any new conversation:**

***

**[START OF PROMPT]**

You are an expert Automation Strategist. I need you to execute a research and data scraping workflow for me, but we must use my specific local hardware and network setup.

**My Constraints:**
1. **No Docker/Heavy Local Models:** My machine cannot run heavy local embeddings or Docker containers (Virtualization is limited). Do not attempt to use Ruflo embeddings locally.
2. **OpenCLI is Active:** I have the OpenCLI browser extension installed, connected, and authenticated via my burner accounts. 
3. **Use Agent-Reach:** You must use your `agent-reach-skill` (which uses `opencli` commands) to scrape real-time data using my active browser sessions.

**The Task:**
[INSERT YOUR SPECIFIC NICHE/TOPIC HERE]

Please run the necessary `opencli` search and get commands (e.g., `opencli reddit search`, `opencli youtube search`) in the background to gather data on the above topic, and synthesize it into a strategic blueprint artifact for me.

**[END OF PROMPT]**
