# 🤖 n8n AI Automation Workflows

A collection of production-ready AI automation workflows built with **n8n**. Each folder contains the exportable workflow JSON, canvas screenshots, sample templates/outputs, and step-by-step setup instructions.

## 📂 Included Workflows

| Workflow | Description | Trigger | Key Integrations |
| :--- | :--- | :--- | :--- |
| **[Daily AI & Tech News Digest](./daily-ai-tech-news-digest)** | Combines AI Business & TechCrunch RSS feeds with SerpApi Google Events, summarizes top news and events via Google Gemini, and delivers a daily brief to Gmail at 10:00 AM. | Schedule (Daily at 10:00 AM) | RSS Feeds, HTTP Request (SerpApi), Google Gemini, Gmail |
| **[LinkedIn Post Generator](./linkedin-post-generator)** | Monitors Google Sheets for new article links, summarizes the content, drafts an industry-expert post via OpenRouter (`GPT-3.5-turbo`), and auto-publishes to LinkedIn. | Google Sheets Trigger (Every Hour) | Google Sheets, OpenRouter, LinkedIn |
| **[Multimodal AI LinkedIn Post & Image Generator](./linkedin-post-generator-with-image)** | Reads article links from Google Sheets, drafts a LinkedIn post with Google Gemini, generates a custom visual via Stability AI, and publishes the text + image post to LinkedIn. | Google Sheets Trigger (Every Minute) | Google Sheets, Google Gemini, HTTP Request (Stability AI), LinkedIn |
| **[Automated LinkedIn Job Tracker](./automated-linkedin-job-tracker)** | Fetches LinkedIn job postings via RSS, extracts required skills and drafts a custom cover letter with Google Gemini, and logs structured rows into Google Sheets. | Schedule (Daily at 10:00 AM) | RSS Feed (FetchRSS), Google Gemini, Structured Output Parser, Google Sheets |
| **[Auto AI Internship Applier](./auto-ai-internship-applier)** | Monitors Google Sheets for new internship entries, drafts a tailored application email using Google Gemini with structured JSON parsing, and sends it via Gmail. | Google Sheets Trigger (`rowAdded` at 10:00 AM) | Google Sheets, Google Gemini, Structured Output Parser, Gmail |
| **[Automated Historical Content Publisher](./automated-historical-content-publisher)** | Dynamically reads today's date, generates an engaging "On This Day in History" post using Google Gemini, and auto-publishes it to LinkedIn every day at 1:00 PM. | Schedule (Daily at 1:00 PM) | Google Gemini, LinkedIn |
| **[AI-Powered Weather-Based Daily Planner](./ai-weather-daily-planner)** | Fetches live city weather from OpenWeatherMap, generates an outfit suggestion, outdoor activity, and weather reminder via Google Gemini, and emails it to Gmail at 1:00 PM. | Schedule (Daily at 1:00 PM) | HTTP Request (OpenWeatherMap), Google Gemini, Gmail |
| **[AI Podcast Generator (Chat to Voice)](./ai-podcast-generator)** | Accepts a topic via n8n Chat, generates a 2-minute conversational podcast script with Google Gemini (`2.5-flash`), and synthesizes downloadable speech via Murf AI. | Chat Trigger | Google Gemini, HTTP Request (Murf AI) |
| **[AI Podcast Generator (Full-Stack Webhook + MellowCast UI)](./ai-podcast-generator-webhook)** | Connects the MellowCast web frontend to an n8n Webhook backend to generate a script via OpenRouter (`Gemini 2.5 Flash Lite`) and stream binary `.wav` audio back to the browser. | Webhook (`POST`) | Webhook, OpenRouter, HTTP Request (Murf AI) |
| **[AI Speech-to-Speech (STS) Audio Summarizer](./ai-speech-to-speech-summarizer)** | Downloads spoken audio from a URL, transcribes it with Groq Whisper (`whisper-large-v3-turbo`), extracts action bullets via Google Gemini, and outputs spoken audio via Murf AI. | Chat Trigger | HTTP Request (Groq Whisper), Google Gemini, HTTP Request (Murf AI) |

## 🚀 How to Import Any Workflow

1. Open your **n8n** instance (Cloud or Self-Hosted).
2. Click **Add Workflow** (`+`) in the top-left corner.
3. Click the **three dots menu (`...`)** in the top-right corner and select **Import from File**.
4. Select the `.json` workflow file from the desired folder.
5. Open each node with a warning icon and attach your own credentials.
