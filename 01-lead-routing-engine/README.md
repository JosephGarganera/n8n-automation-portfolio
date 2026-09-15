# 💼 Portfolio Project 1: The Automated Lead Routing & AI Intent Engine

## 🎯 Executive Summary

This production-grade workflow automates the extraction, enrichment, and intelligent routing of inbound marketing leads. Built to replace high-latency manual sales sorting, the pipeline intercepts incoming lead data arrays, programmatically calculates lead quality tiers, uses a cloud-hosted LLM to determine customer purchasing intent, and deterministically routes high-value prospects to dedicated communication endpoints.

### 📈 Business Impact

- **Latency Reduction:** Cuts lead qualification processing time down from hours to milliseconds.
- **Operational Accuracy:** Employs zero-shot LLM intent classification to systematically filter out low-intent inquiries, ensuring high-value enterprise accounts receive immediate routing priority.

---

## 🗺️ Visual Architecture Map

![n8n Lead Routing Architecture](./workflow-preview.png)

_(To run this automation yourself: 📥 [Download JSON Workflow Blueprint](./workflow.json) and paste it directly onto your n8n canvas.)_

---

## 🛠️ Technical Stack & Versioning

- **Orchestration Platform:** [n8n Workflow Automation Engine](https://n8n.io) (`v2.35.7` Self-Hosted Lifecycle)
- **Artificial Intelligence Layer:** [Groq Cloud API Console](https://groq.com) running high-throughput `Qwen` open-weights LLM topologies.
- **Framework Layer:** LangChain integration via native n8n `Basic LLM Chain` and `Chat Model` nodes.
- **Data Processing Drivers:** JavaScript (ES6+) runtime executing inside secure, sandboxed workflow execution frames.
- **Data Payload Protocols:** Highly structured JSON (JavaScript Object Notation) data streams and objects.

---

## 🔬 Architectural Deep-Dive & Engineering Challenges

### 1. Programmatic Data Transformation via Ternary Expressions

- **Challenge:** Leads arrive with raw quantitative data fields (e.g., `companySize`) that need real-time segmentation without dragging heavy external compute modules into the automation runtime.
- **Solution:** Engineered inline n8n data expressions utilizing condition-based ternary operators: `{{ $json.companySize >= 500 ? 'Enterprise' : 'SMB' }}`. This executes blazing-fast data evaluation at the node layer before routing logic occurs.

### 2. State Retention & Array Synchronization (The Data-Loss Problem)

- **Challenge:** In n8n `v2.35.7`, passing structural data fields through standard LangChain LLM nodes results in data truncation. The node outputs the raw text analysis string from the AI but strips out crucial contextual fields like contact names, email addresses, and metadata.
- **Solution:** Developed an out-of-band state synchronization script inside an isolated **Code Node**. By writing an array map function, the system targets upstream cache layers, programmatically matches transactional index keys, and re-stitches the historical lead data with the new AI intent values cleanly:

```javascript
const currentItems = \$input.all();
const originalLeads = \$('Edit Fields').all();

return originalLeads.map((lead, index) => {
  return {
    json: {
      ...lead.json,
      aiIntent: currentItems[index]?.json?.text?.trim() || "Unknown"
    }
  };
});
```

### 3. Deterministic Routing Frameworks

- **Challenge:** Standard binary `IF` branches scale poorly and create cluttered canvas layouts when trying to split traffic across multiple operational parameters.
- **Solution:** Designed a unified, declarative **Switch Node** pattern using strict matching rules for evaluated strings (`High Intent` / `Low Intent`). This establishes a multi-lane routing matrix that can seamlessly scale out to alternative endpoints (CRMs, webhooks, or messaging channels) from a single structural node.

---

## 🚀 Deployment & Rebalancing Guidelines

1. Import the `workflow.json` blueprint into your local or self-hosted n8n environment.
2. Open the **Groq Chat Model** node and select **Create New Credential**. Insert your secure `Groq API Key`.
3. Set the model parameter type to **Fixed** and select an active text generation model endpoint (e.g., `qwen/qwen3.6-27b` or `llama-3.1-8b-instant`).
4. Click **Execute Workflow** on the `Schedule Trigger` node to run the end-to-end data evaluation engine.
