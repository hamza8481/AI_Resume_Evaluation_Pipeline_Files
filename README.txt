Automated Resume Screening Agent

An end-to-end Applicant Tracking System (ATS) workflow built in n8n. This pipeline fully automates the initial screening of candidates by parsing their submitted CVs, mapping them to the specific Job Description (JD) they applied for, and using AI to objectively evaluate their fit for the role.

Business and Operational Value
1. Automated Resume Parsing: Eliminates manual data entry by extracting core candidate details (skills, experience, education) directly from PDF resumes into structured JSON using AI.
2. Objective Candidate Screening: Maps the extracted resume data against the actual Job Description pulled dynamically from Google Drive.
3. Automated Decision Logic: Evaluates candidates and scores them (out of 10). Automatically triggers Slack notifications for highly qualified candidates (score >= 8) and rejection emails for unqualified ones.
4. Centralized Tracking: Automatically populates an ATS Google Sheet with candidate data, match scores, strengths, and capability gaps.

Tech Stack and Key Nodes
1. Framework: n8n Workflow with Langchain AI nodes.
2. Data Intake: n8n Form Trigger (Publicly accessible).
3. Storage and Lookups: Google Drive (CV uploads and JD downloads) and Google Sheets (JD mapping and ATS tracking).
4. LLM Engine: OpenAI gpt-4o-mini (for fast, cost-effective extraction and evaluation).
5. Notification Routing: Slack and SendGrid.

Execution Flow
1. Candidate Application: The applicant submits their Name, Email, Job Role, and PDF Resume via an n8n web form.
2. Document Archival: The resume is uploaded to a specific Google Drive folder for safe-keeping.
3. Data Extraction: The Profile Analyzer Agent reads the PDF and structures the text into standard ATS JSON format.
4. JD Retrieval: The workflow checks a Google Sheet to find the correct Job Description PDF link for the role they selected, then downloads and extracts the text of the JD.
5. AI Evaluation: The HR Expert Agent compares the JSON resume against the JD text. It generates an overall_fit_score, strengths, and concerns.
6. Post-Processing: The Map Columns node merges the candidates original form details with the AI evaluation.
7. Database Update: The results are inserted into a Google Sheet.
8. Routing: If the score is 8 or above, a Slack alert is sent to the hiring channel. If below 8, a polite rejection email is dispatched via SendGrid.
