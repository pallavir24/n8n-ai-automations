# 🤖 n8n AI Automation Workflows

A collection of production-ready AI automation workflows built with **n8n**. Each folder contains the exportable workflow JSON, canvas screenshots, and setup instructions.

## 📂 Included Workflows

| Workflow | Description | Trigger | Key Integrations |
| :--- | :--- | :--- | :--- |
| **[AI News Summarizer](./ai-news-summarizer)** | Fetches top AI news, generates a concise digest using an LLM, and delivers it to Gmail every morning at 10:00 AM. | Schedule (Daily at 10 AM) | RSS / News API, LLM, Gmail |
| **[LinkedIn Post Generator](./linkedin-post-generator)** | Reads article URLs from Google Sheets, extracts the content, drafts an engaging LinkedIn post, and updates/publishes the result. | Google Sheets / Schedule | Google Sheets, HTTP Request, LLM, LinkedIn |

## 🚀 How to Import Any Workflow

1. Open your **n8n** instance (Cloud or Self-Hosted).
2. Click **Add Workflow** (`+`) in the top-left corner.
3. Click the **three dots menu (`...`)** in the top-right corner and select **Import from File**.
4. Select the `workflow.json` file from the desired folder.
5. Open each node with a warning icon and attach your own credentials.
