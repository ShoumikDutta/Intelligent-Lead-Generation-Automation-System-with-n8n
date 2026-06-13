# Intelligent Lead Generation & Outreach Automation with n8n

An automated lead generation workflow built in **n8n** that collects business search inputs, finds potential leads, extracts contact emails from company websites using an LLM-powered information extractor, stores the results in Google Sheets, and prepares/sends outreach emails through Gmail.

This project was created as a practical automation prototype for a commercial / GTM use case, focused on reducing manual prospect research and making lead preparation faster, more structured, and easier to reuse.

---

## Project Overview

The workflow allows a user to submit a lead search request through an n8n form by entering:

* Business type
* Target location
* Number of leads required
* Preferred email style

After submission, the workflow automatically searches for matching businesses, filters valid leads with websites, extracts email addresses, stores them in a spreadsheet, and sends a predefined outreach email.

---

## Key Features

* Form-based lead search input
* Automated business lead discovery by business type and location
* Website filtering to keep only leads with valid websites
* LLM-assisted email extraction from company websites
* Google Sheets integration for lead storage
* Gmail integration for automated outreach
* Wait/delay step to manage workflow execution timing
* Configurable lead quantity and outreach style
* Designed as a reusable GTM / sales automation workflow

---

## Workflow Architecture

```text
Form Submission
      ↓
HTTP Request to Lead Source / Scraper
      ↓
Filter Leads with Website
      ↓
LLM Information Extractor
      ↓
Wait Step
      ↓
Append Email to Google Sheets
      ↓
Send Outreach Email via Gmail
```

---

## Tech Stack

* **n8n** – workflow automation platform
* **Apify / HTTP Request API** – lead and business data collection
* **OpenRouter / GPT-3.5 Turbo** – LLM-based email extraction
* **Google Sheets** – structured lead storage
* **Gmail** – outreach email sending
* **JSON workflow export** – reusable n8n workflow configuration

---

## Workflow Nodes

### 1. Form Trigger

Collects the user input required to start the lead generation process.

Fields used:

* `Business Type`
* `Location`
* `Lead Number`
* `Email Style`

Example input:

```text
Business Type: IT Services
Location: India
Lead Number: 5
Email Style: Professional
```

---

### 2. HTTP Request

Sends the submitted business type and location to an external lead scraping/search API.

The request is configured to search for places based on:

* Business category
* Location query
* Maximum number of leads

---

### 3. Filter

Filters the returned lead data and keeps only leads where a website exists.

This avoids wasting LLM/API calls on leads that do not have a website available.

---

### 4. Information Extractor

Uses an LLM to extract the best available email address from the company website.

The extracted field is:

```text
Email Address
```

---

### 5. Wait Node

Adds a short delay before writing results to Google Sheets.

This can help with rate limits, execution stability, or API timing.

---

### 6. Google Sheets

Appends the extracted email address to a Google Sheet.

Example output column:

```text
EMAIL ID
```

---

### 7. Gmail

Sends a predefined outreach email to the extracted email address.

The email can be customized based on the campaign, target audience, or business use case.

---

## Example Use Case

A sales or GTM team wants to find IT service companies in a specific location and prepare outreach emails.

Instead of manually searching Google, opening websites, finding email addresses, copying them into a spreadsheet, and drafting emails, this workflow automates the full process:

1. Enter target business type and location.
2. Generate a lead list.
3. Extract contact emails.
4. Store leads in Google Sheets.
5. Send outreach emails automatically.

---

## Business Value

This automation helps reduce repetitive manual work in prospecting and lead preparation.

It can support:

* Sales development representatives
* GTM teams
* Startup founders
* Agencies
* B2B outreach teams
* Freelancers doing prospect research

Main benefits:

* Faster lead research
* More consistent data collection
* Reduced manual copy-paste work
* Reusable outreach process
* Structured lead storage
* Scalable workflow foundation

---

## Setup Instructions

### 1. Clone this repository

```bash
git clone https://github.com/your-username/intelligent-lead-generation-n8n.git
cd intelligent-lead-generation-n8n
```

---

### 2. Import the workflow into n8n

1. Open your n8n instance.
2. Go to **Workflows**.
3. Click **Import from File**.
4. Upload the workflow JSON file.
5. Review all nodes before activating the workflow.

---

### 3. Configure credentials

You need to configure the following credentials in your own n8n instance:

* API key for the lead scraping/search service
* OpenRouter API credentials
* Google Sheets OAuth credentials
* Gmail OAuth credentials

Do not commit real API keys, credential IDs, OAuth tokens, or private spreadsheet links to GitHub.

---

### 4. Update environment-specific values

Before running the workflow, replace placeholders and private values such as:

```text
APIFY_API_KEY
Google Sheet document ID
Gmail account credentials
OpenRouter credentials
Calendar or booking link inside the email body
```

---

### 5. Test the workflow

Use test input such as:

```text
Business Type: IT Services
Location: India
Lead Number: 5
Email Style: Professional
```

Then check:

* Whether leads are returned
* Whether websites are detected
* Whether email addresses are extracted correctly
* Whether rows are added to Google Sheets
* Whether the Gmail node sends the email as expected

---

## Security Notes

Before publishing this project publicly, make sure to remove or replace:

* Real API keys
* OAuth credential IDs
* Gmail account details
* Google Sheet IDs
* Private spreadsheet URLs
* Personal email addresses
* Production webhook URLs
* Any real customer or lead data

For public GitHub repositories, use placeholders such as:

```text
YOUR_APIFY_API_KEY
YOUR_OPENROUTER_CREDENTIAL
YOUR_GOOGLE_SHEET_ID
YOUR_GMAIL_CREDENTIAL
YOUR_BOOKING_LINK
```

---

## Possible Improvements

Future improvements could include:

* Adding duplicate lead detection
* Adding email validation before outreach
* Adding a human approval step before sending emails
* Supporting multiple email templates
* Generating personalized email content using the selected email style
* Adding CRM integration such as HubSpot, Salesforce, or Dynamics 365
* Adding lead scoring based on company profile
* Adding error handling for missing websites or failed API calls
* Adding logging for failed email extraction attempts
* Exporting final leads as CSV

---

## Disclaimer

This project is intended for educational and prototyping purposes.

When using lead generation and outreach automation, make sure to follow applicable privacy, consent, anti-spam, and data protection laws such as GDPR, CAN-SPAM, or other local regulations.

---

## Author

Built as an n8n automation project focused on AI-assisted lead generation, structured prospect research, lead enrichment, and outreach preparation.
