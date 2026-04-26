# WAO Foundation — Website & Automation Stack

Full digital infrastructure built for a non-profit foundation (WAO Foundation). Covers the public-facing website, donor and stakeholder communications, internal reporting, and end-to-end operational process automation. A lean team now operates with the leverage of a much larger one.

---

## Background

The foundation needed a professional web presence and a way to manage communications, reporting, and internal workflows without hiring additional staff. Everything was manual — emails, reports, follow-ups, and coordination all required individual human action. The brief was to automate what could be automated, so the team could focus on mission-critical work.

---

## Architecture

```
┌──────────────────────────────────────┐
│         Public Website               │
│    (WordPress — managed hosting)     │
│  Donation pages, programs, content   │
└───────────────┬──────────────────────┘
                │ Form submissions / triggers
┌───────────────▼──────────────────────┐
│         Automation Layer             │
│            (n8n — self-hosted)       │
│  • Donor acknowledgement emails      │
│  • Stakeholder update sequences      │
│  • Internal reporting workflows      │
│  • Data sync between tools           │
└───────────────┬──────────────────────┘
                │
┌───────────────▼──────────────────────┐
│         Static Assets / CDN          │
│       (Cloudflare Pages)             │
│  Reports, downloadable resources,    │
│  event materials                     │
└──────────────────────────────────────┘
```

---

## Components

### Website (WordPress)
- Full redesign and development on managed WordPress hosting
- Custom theme aligned with the foundation's brand and mission
- Donation and contact forms with n8n webhook integration
- SEO-optimised content structure, sitemap, and metadata
- Mobile-first, accessible design

### Automation Workflows (n8n)
- **Donor Acknowledgement** — Auto-send personalised thank-you email within minutes of a donation form submission
- **Stakeholder Updates** — Scheduled email sequences for programme updates and impact reports
- **Internal Reporting** — Weekly automated summary of form submissions, donor activity, and operational metrics — delivered to the team via email
- **Data Sync** — Connects WordPress form data to Google Sheets for record-keeping and reporting

### Static Asset Hosting (Cloudflare Pages)
- Annual reports, programme brochures, and event materials hosted on Cloudflare Pages
- Fast global delivery via Cloudflare CDN
- Zero-cost static hosting for non-profit budget constraints

---

## Tech Stack

| Layer | Tool |
|---|---|
| Website | WordPress (managed hosting) |
| Forms | WordPress forms with webhook triggers |
| Automation | n8n (self-hosted on Hetzner VPS) |
| Email delivery | SMTP via n8n |
| Static assets | Cloudflare Pages |
| Data logging | Google Sheets |

---

## Key Outcomes

- Website redesigned and launched with professional brand alignment
- Donor acknowledgement emails automated — average response time reduced from days to minutes
- Stakeholder communication sequences replaced manual email drafting
- Weekly internal reports delivered automatically — no staff time required
- Team operates with significantly less administrative overhead, focusing on programme delivery

---

## Status

Delivered and handed over. Ongoing retainer for maintenance and workflow updates.

---

*Built and maintained by [True Hub Solutions](https://truehubsolutions.com)*
