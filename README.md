# 🧾 Invoice Automation Pipeline

### AI-Powered Invoice Processing — From Gmail to Google Sheets, Automatically

*Zero manual data entry. No missed invoices. A clear weekly snapshot of cash flow.*

[![Built with n8n](https://img.shields.io/badge/Built_with-n8n-EA4B71?style=for-the-badge&logoColor=white)](https://n8n.io)
[![Powered by Claude](https://img.shields.io/badge/Powered_by-Claude_AI-D97757?style=for-the-badge&logoColor=white)](https://claude.ai)
[![Google Sheets](https://img.shields.io/badge/Storage-Google_Sheets-34A853?style=for-the-badge&logo=googlesheets&logoColor=white)](https://sheets.google.com)
[![Status](https://img.shields.io/badge/Status-Complete-brightgreen?style=for-the-badge)](https://github.com/Milena-Tanui/invoice-automation-pipeline)

---

## 🧠 What Is This?

A two-workflow automation system that processes 200+ invoices per month with zero manual input. Every invoice email is detected automatically, read by Claude AI, and routed into Google Sheets — sorted by vendor. Every Sunday, the business owner receives a formatted summary email with totals and overdue flags.

---

## 🎯 The Problem It Solves

Businesses receiving hundreds of invoices per month via email face hours of manual sorting, copy-pasting, and tracking every week. A single missed invoice or data entry error can disrupt cash flow visibility.

This pipeline eliminates that burden entirely.

---

## 🎬 Demo Video

> *A short walkthrough of the Invoice Automation Pipeline running live — from Gmail trigger to Google Sheets output and weekly digest email.*

[![Watch the Demo](https://img.shields.io/badge/Watch_Demo-Loom%2FYouTube-FF0000?style=for-the-badge&logo=youtube&logoColor=white)](https://www.loom.com/share/54aabe263a9e4958b9c710f22f6c78c0)

---

## ⚙️ How It Works

Two separate workflows handle two distinct jobs:

### Workflow 1 — Invoice Processing Pipeline (event-driven)

```
New Invoice Email Arrives in Gmail
        ↓
  [Gmail Trigger]
  Detects emails with PDF attachments
        ↓
  [JavaScript Code Node]
  Converts binary PDF to base64 format
  for Claude API compatibility
        ↓
  [Claude API — Anthropic]
  Reads the PDF and extracts structured
  data: vendor, invoice #, amounts, dates
        ↓
  [Confidence Check — IF Node]
  Score ≥ 0.85 → All Invoices tab
  Score < 0.85 → Needs Review tab
        ↓
  [Google Sheets]
  Clean data appended automatically,
  sorted by vendor
```

### Workflow 2 — Weekly Digest (scheduled)

```
Every Sunday at 6PM
        ↓
  [Schedule Trigger]
        ↓
  [Google Sheets — Read Rows]
  Fetches last 7 days of invoice data
        ↓
  [JavaScript Code Node]
  Aggregates totals by vendor,
  flags overdue invoices
        ↓
  [Gmail — Send Message]
  Formatted HTML summary email
  delivered to business owner
```

---

## 🛠️ Stack

| Layer | Tool | Role |
|---|---|---|
| 🔁 **Workflow Orchestration** | n8n | Triggers, routing, scheduling, Sheets integration |
| 🧠 **AI Extraction** | Claude API (Anthropic) | PDF reading and structured JSON output |
| 📊 **Data Storage** | Google Sheets | Vendor-sorted invoice log and review queue |
| ✉️ **Email** | Gmail | Invoice trigger and weekly digest delivery |
| 💻 **Logic** | JavaScript | Binary to base64 conversion, data aggregation |

---

## ✨ Key Features

- 📥 Automatic Gmail monitoring for invoice emails
- 🤖 AI-powered PDF data extraction using Claude
- 🚩 Confidence scoring with human review flagging
- 📊 Vendor-sorted Google Sheets with two tabs
- ⏰ Scheduled weekly digest email every Sunday
- 🔁 Deduplication by invoice number

---

## 📋 Extracted Fields

| Field | Description |
|---|---|
| `vendor_name` | Supplier name |
| `invoice_number` | Unique invoice ID (dedup key) |
| `invoice_date` | Date of issue |
| `due_date` | Payment due date |
| `currency` | Invoice currency |
| `subtotal` | Amount before tax |
| `tax` | Tax amount |
| `total` | Total amount due |
| `confidence` | AI extraction confidence (0–1) |
| `review_reason` | Flagging reason if confidence < 0.85 |

---

## 📁 Workflow Files

| File | Description |
|---|---|
| [`invoice-automation-pipeline.json`](invoice-automation-pipeline.json) | Event-driven invoice processing workflow |
| [`weekly-digest.json`](weekly-digest.json) | Scheduled weekly summary email workflow |

---

## 🚀 Setup Instructions

1. Import `invoice-automation-pipeline.json` into your n8n instance
2. Import `weekly-digest.json` into your n8n instance
3. Connect your Gmail account in both workflows
4. Add your Anthropic API key to the HTTP Request node headers
5. Connect your Google Sheets account and set your spreadsheet ID
6. Activate both workflows

> ⚠️ Never commit your API key to GitHub. Replace it with `YOUR_ANTHROPIC_API_KEY` in the JSON file before uploading.

---

## 📸 Screenshots

### Workflow 1 — Invoice Processing Pipeline
![Invoice Pipeline Workflow](workflow-canvas.jpg)

### Google Sheets Output
![Google Sheets](google-sheets.jpg)

### Workflow 2 — Weekly Digest Pipeline
![Weekly Digest Workflow](digest-workflow.jpg)

### Weekly Digest Email
![Weekly Digest Email](digest-email.jpg)

---

## 🔭 Future Enhancements

- **OCR support** — handle scanned/image-only PDFs via Google Document AI
- **Multi-currency conversion** — auto-convert all totals to a base currency
- **Slack notifications** — alert the owner instantly when a high-value invoice arrives
- **Vendor dashboard** — a summary view per vendor across multiple months

---

## 💡 Built By

**Milena Tanui** — AI Agent Builder & Workflow Automation Specialist

> *"Built using a low-code approach: prompt engineering drives the AI extraction logic, n8n handles orchestration and scheduling, and Google Sheets provides zero-setup data storage."*

[![GitHub](https://img.shields.io/badge/GitHub-Milena--Tanui-181717?style=for-the-badge&logo=github)](https://github.com/Milena-Tanui)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Connect-0A66C2?style=for-the-badge&logo=linkedin)](https://www.linkedin.com/in/milena-tanui-64b898173)
[![Portfolio](https://img.shields.io/badge/Portfolio-Visit-D97757?style=for-the-badge)](https://milena-tanui.github.io/Portfolio/)

---

*Part of a growing portfolio of AI agents and automation tools.*
**⭐ Star this repo if you find it useful!**
