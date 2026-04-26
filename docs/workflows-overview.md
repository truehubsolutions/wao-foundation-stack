# Workflows Overview — WAO Foundation Automation

High-level map of all automation workflows in the stack. Each workflow is a discrete n8n flow with its own trigger, logic, and outputs.

---

## Workflow Inventory

| # | Workflow | Trigger | Output | Status |
|---|---|---|---|---|
| 1 | Donor Acknowledgement | WordPress form submission (webhook) | Personalised email to donor + Google Sheets log | Active |
| 2 | Weekly Internal Report | Schedule — every Monday 08:00 PHT | HTML summary email to management | Active |
| 3 | Stakeholder Update Sequence | Manual trigger | Personalised email to each stakeholder | Active |

---

## Trigger Decision Map

```
Something happens on the website
  └── Is it a form submission?
        ├── YES → Webhook fires → Which form?
        │           ├── Donation form → Workflow 1 (Donor Ack)
        │           └── Contact form → Logged to Sheets only
        └── NO → Not automated (handled manually)

Is it Monday morning?
  └── YES → Schedule fires → Workflow 2 (Weekly Report)

Does the team need to send a programme update?
  └── YES → Manual trigger → Workflow 3 (Stakeholder Update)
```

---

## Data Logged per Workflow

### Workflow 1 — Donor Acknowledgement

| Field | Source | Logged to Sheets |
|---|---|---|
| Name | Form input | ✓ |
| Email | Form input | ✓ |
| Donation amount | Form input | ✓ |
| Programme | Form input | ✓ |
| Timestamp | n8n system | ✓ |
| Email sent? | n8n result | ✓ |

### Workflow 2 — Weekly Report

Aggregates the Sheets data above. No additional logging.

### Workflow 3 — Stakeholder Update

| Field | Source | Logged to Sheets |
|---|---|---|
| Recipient name | Sheets (stakeholder list) | — |
| Email sent timestamp | n8n result | ✓ |
| Campaign/update name | Manual input at trigger | ✓ |

---

## Error Handling

- **Email delivery failure:** n8n retries 3 times with exponential backoff. On final failure, an error notification is sent to the admin email.
- **Webhook unavailable:** WordPress form stores submissions locally; n8n picks them up on next successful connection.
- **Sheets write failure:** n8n execution is flagged as failed in the Executions log. Admin reviews and re-runs manually.

---

## Planned Improvements

- [ ] Add SMS fallback for donor acknowledgements (Twilio)
- [ ] Segment weekly report by programme area
- [ ] Automate stakeholder sequence on a drip schedule instead of manual trigger
