# 📰 Daily AI, Tech News & Events Digest (to Gmail)

An automated n8n intelligence workflow that pulls the latest news from **AI Business** and **TechCrunch** alongside live event listings from **SerpApi (Google Events)**, summarizes and categorizes everything using **Google Gemini**, and delivers a daily brief to **Gmail** at **10:00 AM**.

![Workflow Canvas](./workflow-canvas.png)

## ⚙️ How It Works

1. **Schedule Trigger:** Runs automatically every day at **10:00 AM** (`triggerAtHour: 10`).
2. **Multi-Source Data Ingestion (3 Parallel Branches):**
   * **AI Business (`RSS Read`):** Fetches the latest 50 AI news articles (`https://aibusiness.com`).
   * **TechCrunch (`RSS Read1`):** Fetches the latest 20 broader tech articles (`https://techcrunch.com`).
   * **SerpApi Google Events (`Fetch Request`):** Queries `https://serpapi.com` (`engine: google_events`, `q: Events in India`) to pull upcoming local/regional events.
3. **Merge (`append` - 3 Inputs):** Combines all 3 streams into a single unified list (71 items total).
4. **Aggregate:** Consolidates all items into one payload, extracting `title`, `link`, and `contentSnippet` to optimize token usage.
5. **AI Intelligence Report (`Basic LLM Chain` + `Google Gemini Chat Model`):** Uses **Google Gemini** with strict grounding rules (no hallucinated content) to format the digest into three clean sections:
   * **AI News Highlights** (Top 5 AI developments)
   * **Technology Updates** (Latest broader tech news)
   * **Upcoming AI Events** (Date, location, description, and link)
6. **Send Email (`Send a message`):** Delivers the formatted plain-text intelligence report via **Gmail** with the subject `"AI News"`.

## 🔑 Required Credentials & API Keys

Configure the following in n8n after importing the workflow:
* **Google Gemini (PaLM) API:** Required for the `Google Gemini Chat Model` node.
* **SerpApi API Key:** Required in the `Fetch Request` (HTTP Request) node under the `api_key` query parameter.
* **Gmail OAuth2:** Required for the `Send a message` node to send the daily email.

## 🛠️ Setup Instructions

1. Import `workflow.json` into your n8n instance.
2. Open the **Schedule Trigger** node and verify that your n8n timezone matches your local **10:00 AM**.
3. Open the **Fetch Request** node, paste your **SerpApi API key** into the `api_key` query parameter, and optionally customize the `q` parameter (currently set to `Events in India`).
4. Open the **Google Gemini Chat Model** node and attach your Google Gemini API credentials.
5. Open the **Send a message** (Gmail) node, connect your Gmail account, and enter your recipient email address in the **To** field.
6. Click **Test Workflow** to verify the email delivery, then toggle the workflow to **Active**.

## 📧 Sample Email Output

```text
Hi there,
Here's your Tech Brief:

AI NEWS HIGHLIGHTS

ANTHROPIC IPO TESTS WALL STREET'S APPETITE FOR STANDALONE FRONTIER AI
The public offering will gauge investor confidence in AI vendors and highlight the financial risks and infrastructure commitments for enterprise customers.
Link: <https://aibusiness.com/foundation-models/anthropic-ipo-tests-wall-street-s-appetite-for-frontier-ai>

OPENAI, GOOGLE PARTNERSHIP TARGETS ENTERPRISE MODEL CHOICE
OpenAI has expanded its enterprise strategy by making its models available on all three major cloud provider platforms.
Link: <https://aibusiness.com/generative-ai/openai-google-partnership-enterprise-model-choice>

DEEPSEEK MAKES DEEPINFER OPEN SOURCE TO CUT AI COSTS
The Chinese AI vendor is moving to gain an advantage in the open-source market while addressing enterprise concerns regarding high token rates.
Link: <https://aibusiness.com/generative-ai/deepseek-makes-deepinfer-open-source-cut-ai-costs>

TECHNOLOGY UPDATES

JENSEN HUANG’S SCANDAL-FUELED OUSTER EXPOSES ENTERPRISE DOUBTS ABOUT AI
The leadership shakeup at Nvidia highlights lurking industry risks as enterprises navigate unclear returns on investment for AI technology.
Link: <https://aibusiness.com/data-centers/jensen-huang-s-ouster-exposes-ai-doubts>

AGILITY ROBOTICS GOES PUBLIC AS FIRST U.S. SPECIALIST HUMANOID MAKER
The company has entered the public markets supported by more than $300 million in conditional multiyear orders for its Digit 5 humanoid robot.
Link: <https://aibusiness.com/robotics/agility-robotics-goes-public-first-u-s-specialist-humanoid-maker>

CHINA’S BLOCK OF SOFTBANK’S ABB PURCHASE RAISES SUPPLY-CHAIN QUESTIONS
The move to stop this major acquisition has sparked international concerns regarding the future of cross-border investment in the robotics sector.
Link: <https://aibusiness.com/automation/china-s-block-of-softbank-s-abb-purchase>

UPCOMING AI EVENTS

No AI events scheduled this week

Your AI Intelligence Team

---
This email was sent automatically with n8n
https://n8n.io
```
