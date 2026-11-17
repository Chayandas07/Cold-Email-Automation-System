# Cold Email Automation System

A Python based Google Colab project demonstrating Gmail API integration, OAuth 2.0 authentication, contact-file processing, personalized HTML email generation, batch processing, retry handling, campaign cancellation, and CSV reporting.

> **Responsible use:** Use this project only to contact people you are permitted to contact. Follow applicable privacy, anti spam, and email marketing laws. Respect opt out requests. Keep dry run mode enabled while testing. This repository is a learning and portfolio project, not a production email marketing platform.

## Features

- Gmail API integration using OAuth 2.0 and the `gmail.send` scope.
- CSV and Excel contact file upload and processing.
- Email-address validation and duplicate removal.
- Personalized HTML email templates.
- Batch processing with configurable sequence limits.
- Retry handling for selected temporary Gmail API errors.
- Campaign cancellation.
- CSV-based activity and send reporting.
- Dry-run mode to preview actions before live sending.

## Repository Structure

```text
cold-email-automation/
├── cold_email_automation_github_ready.ipynb
├── README.md
├── requirements.txt
├── .gitignore
└── LICENSE
```

## Technology Stack

- Python
- Google Colab / Jupyter Notebook
- Gmail API
- Google OAuth 2.0
- Pandas
- Google API Python Client
- OpenPyXL

## Prerequisites

- A Google account authorized to send email.
- A Google Cloud project with the Gmail API enabled.
- An OAuth 2.0 Desktop application client.
- Python 3.10+ for local dependency installation (Google Colab provides its own runtime).

## Installation

Clone the repository:

```bash
git clone https://github.com/YOUR_GITHUB_USERNAME/cold-email-automation.git
cd cold-email-automation
```

Install dependencies:

```bash
pip install -r requirements.txt
```

Replace `YOUR_GITHUB_USERNAME` with your GitHub username.

## Google OAuth Setup

1. Open the Google Cloud Console and select or create a project.
2. Enable the Gmail API.
3. Configure the OAuth consent screen.
4. Add the following scope:

   ```text
   https://www.googleapis.com/auth/gmail.send
   ```

5. Create an OAuth 2.0 Desktop application client.
6. Download the client credentials JSON file and keep it private.
7. Generate an OAuth token locally and upload `token.json` when the notebook requests it.

**Security:** Never commit `credentials.json`, `token.json`, OAuth client secrets, access tokens, contact files, or private send logs. The `.gitignore` file excludes common sensitive filenames, but review staged files before every commit.

## Running the Notebook

1. Open `cold_email_automation.ipynb` in Google Colab or Jupyter Notebook.
2. Run the cells in order.
3. Upload your OAuth token when prompted.
4. Upload a CSV or Excel contact file.
5. Review the detected contacts, invalid addresses, duplicates, suppression status, templates, and campaign configuration.
6. Keep dry-run mode enabled while testing.
7. Do not enable live sending until you have reviewed the recipients, message content, applicable legal basis, and opt out records.

## Contact File Format

The notebook accepts CSV and Excel contact files. A recommended CSV format is:

```csv
first_name,email,unsubscribed
Taylor,taylor@example.com,false
Jordan,jordan@example.com,true
```

The `email` column is required. `first_name` is used for personalization when available. Set `unsubscribed` to `true` for contacts who must be suppressed.

The notebook does not automatically monitor incoming replies or process unsubscribe replies. Maintain the suppression list manually unless you implement and test reply processing.

## Configuration

The notebook includes settings for:

- Authorized sender email and display name.
- Follow-up interval.
- Maximum email sequence.
- Delay between sends.
- Retry count and retry backoff.
- Dry run mode.

Review all settings before each run. Avoid sending repeated unsolicited messages at short intervals.

## Limitations

- The timer based scheduler depends on the Google Colab runtime remaining active and is not persistent.
- Scheduled jobs may not survive a runtime disconnect or reset.
- Campaign state is not stored in a persistent database by default.
- Duplicate-send protection across runtime restarts is not guaranteed.
- Automatic inbox reply detection and unsubscribe-reply processing are not implemented.
- Gmail API acceptance does not guarantee inbox placement, reading, or recipient side delivery.

These limitations should be addressed before using the project for unattended or production workflows.

## Security Checklist

- [ ] Remove OAuth credentials and tokens from the repository.
- [ ] Remove real contact files, recipient addresses, and private send logs.
- [ ] Clear notebook outputs that may contain sensitive information.
- [ ] Review files staged for commit.
- [ ] Check Git history for previously committed secrets.
- [ ] Use test accounts you control when validating email sending.


## License

This project is distributed under the MIT License. See the `LICENSE` file for details.

