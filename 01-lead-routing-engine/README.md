I. Project Title & Executive Summary

- What it is: A bold title and a 2-3 sentence overview of the automation.
- The Business Impact: Frame it around business metrics. Instead of saying "This routes leads," write: "An automated lead management engine that reduces response latency from hours to seconds by dynamically grading company sizing and using LLMs to isolate high-intent buyer inquiries."

II. Visual Architecture Map

- Place a clean screenshot (workflow-preview.png) of your n8n canvas here. Non-technical recruiters can instantly digest your design patterns, node grouping, and pipeline layout.

III. The Technical Stack & Versioning
Explicitly state your build parameters. This rules out compatibility issues and showcases technical accuracy:

- n8n Core Build: v2.35.7 (Self-Hosted)
- AI Engine: Qwen-2.5 via Groq Cloud API (Using the Basic LLM Chain node infrastructure)
- Custom Code Drivers: JavaScript (ES6+) array transformation mapping

IV. Architectural Deep-Dive (Your Technical Challenges)
This is the most critical section for an engineering manager. Explain the engineering hurdles you faced and how you fixed them:

- Example: Challenge: The LangChain LLM Node outputs isolated text fields, stripping out the parent contact records. Solution: Engineered a targeted JavaScript data mapping sequence inside a specialized Code Node to synchronize upstream arrays with real-time LLM outputs using transactional index positioning.

V. Setup & Deployment Guidelines

- Give clear instructions on how to replicate your work.
- Mention exactly where they need to insert their own API keys or update dropdown parameters to make the blueprint functional.
