# Email Templates — WAO Foundation Automation

All outbound emails use these templates. Variables are injected by n8n using `={{ $json.fieldName }}` expressions.

---

## Donor Acknowledgement

**Subject:** Thank you for supporting WAO Foundation, {{ firstName }}!

```html
<p>Dear {{ firstName }},</p>

<p>Thank you so much for your generous support of the WAO Foundation. Your contribution means a great deal to us and to the communities we serve.</p>

<p>Here is a summary of your donation:</p>
<ul>
  <li><strong>Amount:</strong> {{ donationAmount }}</li>
  <li><strong>Programme:</strong> {{ programme }}</li>
  <li><strong>Date:</strong> {{ donationDate }}</li>
</ul>

<p>We will be in touch with updates on how your contribution is making an impact. In the meantime, feel free to reach out to us at <a href="mailto:info@waofoundation.org">info@waofoundation.org</a>.</p>

<p>With gratitude,<br>
The WAO Foundation Team</p>
```

---

## Weekly Internal Report

**Subject:** WAO Foundation — Weekly Activity Report ({{ weekEnding }})

```html
<h2>Weekly Activity Summary</h2>
<p><strong>Week ending:</strong> {{ weekEnding }}</p>

<h3>Donations</h3>
<ul>
  <li>Total received: {{ totalDonations }}</li>
  <li>New donors: {{ newDonors }}</li>
  <li>Returning donors: {{ returningDonors }}</li>
</ul>

<h3>Enquiries & Contact Forms</h3>
<ul>
  <li>New enquiries: {{ newEnquiries }}</li>
  <li>Responded: {{ responded }}</li>
  <li>Pending: {{ pending }}</li>
</ul>

<h3>Programme Breakdown</h3>
<p>{{ programmeSummary }}</p>

<p><em>This report is automatically generated every Monday morning.</em></p>
```

---

## Stakeholder Programme Update

**Subject:** Programme Update from WAO Foundation — {{ programmeTitle }}

```html
<p>Dear {{ firstName }},</p>

<p>We wanted to share an update on our <strong>{{ programmeTitle }}</strong> programme.</p>

<p>{{ programmeUpdateBody }}</p>

<p>Thank you for your continued support and partnership. If you have any questions, please don't hesitate to reach out.</p>

<p>Warm regards,<br>
The WAO Foundation Team</p>
```
