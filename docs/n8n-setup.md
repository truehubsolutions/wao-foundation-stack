# n8n Workflow Setup Guide — WAO Foundation

This guide covers how to set up the automation stack from scratch on a fresh n8n instance.

---

## Prerequisites

- Self-hosted n8n (v1.0+) running on a VPS or cloud instance
- WordPress site with a form plugin that supports webhook output (e.g. WPForms, Gravity Forms, Contact Form 7 + Webhook)
- SMTP credentials for email delivery (or Resend/SendGrid)
- Google account with Sheets API enabled
- Cloudflare Pages project (for static assets)

---

## Credentials to Configure in n8n

Before importing any workflows, set up these credentials in n8n Settings → Credentials:

| Credential name | Type | Used for |
|---|---|---|
| `WAO SMTP` | SMTP | Email delivery |
| `WAO Google Sheets` | Google Sheets OAuth2 | Data logging |
| `WAO WordPress` | HTTP Header Auth | WP REST API calls |

---

## Workflow 1 — Donor Acknowledgement

**Trigger:** WordPress form submission (webhook)
**Flow:**
1. Webhook receives donor form data
2. Parse: name, email, donation amount, programme
3. Send personalised acknowledgement email (see `templates/donor-ack.html`)
4. Log to Google Sheets: timestamp, name, email, amount, programme

**Import:** Upload `workflows/donor-acknowledgement.json` to n8n → Workflows → Import

**After import:**
- Re-wire `WAO SMTP` credential to the Send Email node
- Re-wire `WAO Google Sheets` credential to the Sheets node
- Activate the workflow
- Copy the webhook URL and paste into your WordPress form's webhook field

---

## Workflow 2 — Weekly Internal Report

**Trigger:** Schedule (every Monday 08:00 PHT)
**Flow:**
1. Pull last 7 days of form submissions from Google Sheets
2. Aggregate: total donations, new contacts, programme breakdown
3. Format into HTML summary report
4. Email to management distribution list

**Import:** Upload `workflows/weekly-report.json`

**After import:**
- Update the Schedule node timezone to `Asia/Manila` (or your local timezone)
- Update recipient email addresses in the Send Email node
- Re-wire credentials
- Activate

---

## Workflow 3 — Stakeholder Update Sequence

**Trigger:** Manual (run when a programme update is ready to send)
**Flow:**
1. Fetch stakeholder list from Google Sheets
2. Loop through each contact
3. Send personalised programme update email
4. Log send timestamp back to Sheets

**Import:** Upload `workflows/stakeholder-update.json`

---

## Testing

After activating each workflow, test with a real form submission (or use n8n's built-in Test Webhook feature) before going live. Check the Executions log in n8n to verify each node completed successfully.

---

## Cloudflare Pages (Static Assets)

Reports and downloadable resources are hosted on Cloudflare Pages:

1. Build your static files locally (PDFs, reports, brochures)
2. Run: `npx wrangler pages deploy <folder> --project-name=wao-assets`
3. Files are available at `https://wao-assets.pages.dev/<filename>`
4. Use these URLs in your email templates for download links
