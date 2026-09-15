# 📊 Portfolio Project 2: The Multi-Source Automated Intelligence Scraper Engine

## 🎯 Executive Summary

This production-grade workflow showcases a parallel data extraction and intelligence engine built to monitor financial and technological landscapes simultaneously. Built to replicate how an enterprise tracks real-time trends, the system runs a split-trigger parallel architecture: one lane tracks high-volatility financial asset fluctuations and builds an inline dashboard table, while a second lane scrapes live software engineering discussions from a raw developer database. The data models are fused via a relational cross-join and summarized using a throttled cloud LLM framework.

### 📈 Business Impact

- **Unified Business Intel:** Fuses disjointed industry data models into a single executive digest payload, removing the need for manual context switching across multiple web apps.
- **Infrastructure Resilience:** Throttles outbound request traffic natively to operate smoothly within tight free-tier API parameters, avoiding operational downtime from rate-limit bans.

---

## 🗺️ Visual Architecture Map

![n8n Scraper Engine Architecture](./workflow-preview.png)

_(To deploy this blueprint: 📥 [Download JSON Workflow Blueprint](./workflow.json) and paste it straight onto your n8n workspace canvas.)_

---

## 🛠️ Technical Stack & Frameworks

- **Orchestration Framework:** [n8n Workflow Automation Platform](https://n8n.io) (`v2.35.7` Self-Hosted Lifecycle)
- **API Interfacing Protocols:** RESTful `GET` data collection streaming clean JSON payloads.
- **Security & Traffic Masking:** Header injection executing automated **User-Agent browser footprint masks**.
- **Data Processing Drivers:** JavaScript (ES6+) runtime executing array transformations (`.slice()` and `.map()`).
- **Artificial Intelligence Layer:** [Groq Cloud Console API Gateway](https://groq.com) running open-weights `Qwen` LLM topologies.

---

## 🔬 Architectural Deep-Dive & Engineering Challenges

### 1. Reverse-Engineering Web Targets & Browser Masking (Option A)

- **Challenge:** Modern web assets employ traffic filters that return broad HTML layouts (`<!DOCTYPE html>`) or drop incoming automated data extraction attempts if a pipeline doesn't identify itself properly.
- **Solution:** Used Chrome Developer Tools (`Network > Fetch/XHR`) to isolate the platform's background data engines. Re-routed n8n to hit the precise API endpoints directly while enforcing an explicit browser footprint configuration inside the HTTP Request headers row:
  - **Name:** `User-Agent`
  - **Value:** `Mozilla/5.0 (Windows NT 10.0; Win64; x64)`

### 2. Multi-Stage Asynchronous Enrichment Looping (Option B)

- **Challenge:** High-performance developer registries (like Hacker News via Firebase) split index tracking from readable datasets, outputting raw flat arrays of 500 numeric IDs (`[49701004, 49701015...]`). Visual nodes fail to map these arrays without throwing schema exceptions.
- **Solution:** Engineered a targeted array-trimming algorithm inside a sandboxed **Code Node**. This slices the incoming array down to the top 5 trending files to protect server memory limits, and wraps each naked number inside an n8n-compliant JSON block for dynamic downstream loop indexing:

```javascript
const allItems = \$input.all();

return allItems.slice(0, 5).map(item => {
  return {
    json: {
      storyId: item.json
    }
  };
});
```

### 3. Cartesian Merge Concurrency Errors & Structural Mismatches

- **Challenge:** Merging a single compiled string entity (Option A's HTML Table) with a 5-item dataset array (Option B's Headlines) causes standard appending systems to overwrite keys. Furthermore, running an unchecked **Cross-Join (All Possible Combinations)** across loose arrays can trigger exponential looping loops that freeze workflow engines.
- **Solution:** Standardized the inputs via a parallel trigger layout configuration and locked the **Merge Node** tracking bounds strictly to a position-based combination strategy. This joins the metrics cleanly, ensuring subsequent nodes have a unified view across both sources within a single payload frame.

### 4. Overcoming Free-Tier AI Rate Limits (TPM Mitigations)

- **Challenge:** Because the Merge node outputs an array of 5 separate rows, n8n attempts to execute 5 concurrent outbound calls to the Groq server at the exact same millisecond. The heavy weight of our embedded HTML table payload overloads free-tier limits, throwing a `429 Rate Limit Reached (Tokens Per Minute)` error.
- **Solution:** Advanced the setup architecture into a restricted serialized sequence. By accessing the **Batch Processing** configurations within the LangChain LLM execution block and throttling the **Batch Size** to exactly `1`, n8n forces the system to queue requests sequentially rather than slamming the AI server simultaneously.

---

## 🚀 Deployment & Rebalancing Guidelines

1. Import the `workflow.json` blueprint file into your local or self-hosted n8n engine workspace canvas.
2. Open the **HTTP Request** nodes and verify the endpoint URLs are active.
3. Access your **Groq Chat Model** node settings, input your secure API credential profile key, and switch the model selector to an active text engine (e.g., `qwen/qwen3.6-27b`).
4. Ensure the Merge node is locked to **All Possible Combinations**, and verify the LLM batch framework size parameter is set to `1`.
5. Execute the **Schedule Trigger** to run the multi-source pipeline end-to-end.
