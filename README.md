Project Overview

Onebox Email Aggregator is a real-time email synchronization system that aggregates multiple IMAP email accounts, provides full-text search capabilities using Elasticsearch, categorizes emails using AI, and integrates with Slack and Webhooks. It also includes AI-powered suggested replies using OpenAI GPT-4.
Architecture Details

System Architecture

The system consists of the following major components:
1.	IMAP Email Fetching: Uses IMAP IDLE mode to fetch emails in real-time from multiple accounts.
2.	Elasticsearch Storage: Stores emails in an indexed format to enable fast searching.
3.	AI Email Categorization: Uses GPT-4 to classify emails into predefined categories.
4.	Slack & Webhook Integration: Sends notifications for important emails.
5.	Frontend (React.js): Displays emails, provides search functionality, and shows AI categorizations.
6.	AI Suggested Replies: Uses RAG (Retrieval-Augmented Generation) to generate responses based on stored context.
   
Technology Stack

•	Backend: FastAPI (Python)
•	IMAP Handling: imaplib (Python)
•	Database: PostgreSQL for metadata, Elasticsearch for full-text search
•	AI Model: OpenAI GPT-4 for email categorization & suggested replies
•	Frontend: React.js with Axios for API requests
•	Real-time Updates: WebSockets or polling (future enhancement)
•	Hosting: Docker (for Elasticsearch, backend, and frontend)

Setup Instructions

1. Install Required Dependencies
Run the following command to install the required Python packages:
pip install fastapi uvicorn imapclient elasticsearch openai requests python-dotenv

2. Setup Elasticsearch
Run Elasticsearch in a Docker container:
docker run -d -p 9200:9200 -e "discovery.type=single-node" docker.elastic.co/elasticsearch/elasticsearch:7.10.1

3. Create a `` File
Create a .env file in the root directory and add:
EMAIL_USERNAME=your-email@gmail.com
EMAIL_PASSWORD=your-app-password
OPENAI_API_KEY=your-openai-api-key
SLACK_WEBHOOK_URL=https://hooks.slack.com/services/YOUR/SLACK/WEBHOOK

4. Run FastAPI Backend
Start the FastAPI server:
uvicorn app:app --reload

5. Run Frontend (React.js)
Navigate to the frontend folder and run:
npm install
npm start

Feature Implementations

1. Real-Time IMAP Email Sync
•	Uses IMAP IDLE mode to listen for new emails.
•	Fetches the last 30 days of emails.
•	Stores email metadata in Elasticsearch.

2. Searchable Email Storage
•	Emails are stored in Elasticsearch for full-text searching.
•	Supports filtering by folder & account.

3. AI Email Categorization
•	GPT-4 categorizes emails into: 
o	Interested
o	Meeting Booked
o	Not Interested
o	Spam
o	Out of Office

4. Slack & Webhook Integration
•	Sends Slack notifications for every "Interested" email.
•	Triggers webhooks for external automation.

5. Frontend Interface (React.js)
•	Displays emails, filters, and AI categorizations.
•	Implements basic search functionality powered by Elasticsearch.

6. AI-Powered Suggested Replies
•	Uses RAG (Retrieval-Augmented Generation) with GPT-4.
•	Suggests context-aware email replies.

API Endpoints

Endpoint	Method	Description
/	GET	Root endpoint
/sync-emails/	GET	Sync emails in the background
/search/?query=text	GET	Search emails by query
/categorize/	POST	Categorize an email
/suggest-reply/	POST	Generate an AI-powered reply

Next Steps

•	Deploy on AWS/GCP using Docker.
•	Implement WebSockets for real-time updates.
•	Enhance AI categorization with fine-tuned models.
•	Improve frontend UI with additional filters and analytics.
This document serves as a comprehensive guide to setting up and running the Onebox Email Aggregator project.

