# 🎯 Automated LinkedIn Job Tracker

An automated n8n workflow that fetches new LinkedIn job listings via RSS every morning, analyzes the job description using **Google Gemini (`gemini-3.5-flash-lite`)** to extract required technical skills and write a tailored 250–300 word cover letter, and logs everything cleanly into **Google Sheets** without duplicates.

![Workflow Canvas](./workflow-canvas.png)

## ⚙️ How It Works

1. **Schedule Trigger:** Runs automatically every day at **10:00 AM** (`triggerAtHour: 10`).
2. **RSS Read:** Fetches the latest job postings from a custom LinkedIn job search RSS feed (generated via **FetchRSS**).
3. **AI Analysis & Cover Letter Drafting (`Basic LLM Chain`):** Uses **Google Gemini (`models/gemini-3.5-flash-lite`)** paired with a **Structured Output Parser** to:
   * Extract company details and full role responsibilities.
   * Identify both explicitly mentioned and implicit technical skills.
   * Generate a personalized **250–300 word cover letter** structured into Opening, Middle, and Closing paragraphs.
4. **Log to Google Sheets (`Append or update row in sheet`):** Writes each job entry into `Sheet1` of your tracker spreadsheet, matching on the **`Link`** column so existing job postings are updated rather than duplicated.

## 📊 Google Sheet Setup

Create a Google Sheet (`Sheet1`) with the exact column headers below before running the workflow:

| Title | Link | Published Date | About Company | job description | skills | cover letter |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| *(Auto-filled)* | *(Unique Match Key)* | *(Auto-filled)* | *(Auto-filled)* | *(Auto-filled)* | *(Auto-filled)* | *(Auto-filled)* |

## 🔑 Required Credentials

Configure the following credentials in n8n after importing the workflow:
* **Google Gemini (PaLM) API:** Required for the `Google Gemini Chat Model` node (`models/gemini-3.5-flash-lite`).
* **Google Sheets OAuth2:** Required for the `Append or update row in sheet` node.
* **Custom RSS Feed URL:** Generate a LinkedIn job search RSS URL using a service like [FetchRSS](https://fetchrss.com) and paste it into the **RSS Read** node.

## 🛠️ Setup Instructions

1. Create a Google Sheet named `Automated LinkedIn Job Tracker` with the 7 column headers listed above.
2. Import `workflow.json` into your n8n instance.
3. Open the **RSS Read** node and paste your custom LinkedIn job search RSS feed URL.
4. Open the **Google Gemini Chat Model** node and attach your Google Gemini API credentials.
5. Open the **Append or update row in sheet** node, connect your Google account, select your Spreadsheet (`Document`) and `Sheet1`, and verify that **`Link`** is set as the matching column.
6. Click **Test Workflow** to verify that job listings, extracted skills, and cover letters populate your sheet, then toggle the workflow to **Active**.
