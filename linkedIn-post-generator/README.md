# 💼 Social Media Automation: AI LinkedIn Post Generator

An automated n8n workflow that monitors a Google Sheet for new article links, summarizes the article, drafts an industry-expert LinkedIn post using **OpenRouter (`openai/gpt-3.5-turbo-0613`)**, and publishes it directly to your LinkedIn profile.

![Workflow Canvas](./workflow-canvas.png)

## ⚙️ How It Works

1. **Google Sheets Trigger:** Polls `Sheet1` in your connected Google Sheet **every hour** for new rows containing an `Article link`.
2. **Article Summarization (`Basic LLM Chain`):** Passes the `Article link` to **OpenRouter (`openai/gpt-3.5-turbo-0613`)** to generate a concise summary of the article.
3. **LinkedIn Post Drafting (`Basic LLM Chain1`):** Sends the summary to a second **OpenRouter (`openai/gpt-3.5-turbo-0613`)** chain with an industry-expert persona prompt to generate a structured post with analysis, industry implications, and a call to action.
4. **Auto-Publish (`Create a post`):** Automatically publishes the generated text directly to your personal **LinkedIn** profile.

## 📊 Google Sheet Setup

Create a Google Sheet (`Sheet1`) with the exact column header below before running the workflow:

| Article link |
| :--- |
| `https://online.hbs.edu/blog/post/ethical-considerations-of-ai` |

## 🔑 Required Credentials

Configure the following credentials in n8n after importing the workflow:
* **Google Sheets Trigger OAuth2:** To monitor your spreadsheet for newly added rows.
* **OpenRouter API:** To power both LLM chains (`openai/gpt-3.5-turbo-0613`).
* **LinkedIn OAuth2:** To publish the final post directly to your LinkedIn profile.

## 🛠️ Setup Instructions

1. Create a Google Sheet with a column named **`Article link`**.
2. Import `workflow.json` into your n8n instance.
3. Open the **Google Sheets Trigger** node, connect your Google account, and select your Spreadsheet (`Document`) and Sheet (`Sheet1`).
4. Open both **OpenRouter Chat Model** nodes and attach your OpenRouter API credentials.
5. Open the **Create a post** (LinkedIn) node, connect your LinkedIn OAuth2 account, and select your profile under **Person**.
6. Add a test link to your Google Sheet, click **Test Workflow** to verify, and toggle the workflow to **Active**.

## 📝 Example Generated Post

> 🚀 **AI agents are shifting from chatbots to autonomous workflows.**
>
> Recent breakthroughs show how businesses are automating repetitive content pipelines while maintaining editorial quality:
> • Event-driven triggers eliminate manual copy-pasting across tools
> • Chained LLM prompts separate research summarization from brand voice drafting
> • Direct API publishing turns raw links into consistent thought leadership
>
> How are you integrating AI automation into your daily content workflow? 👇
>
> #AI #Automation #n8n #ArtificialIntelligence #FutureOfWork
