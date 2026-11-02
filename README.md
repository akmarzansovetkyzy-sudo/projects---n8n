# Contract Generator and Blog Publishing: n8n workflows

Sanitized copies of automation workflows built with n8n. All company names, domains, tokens, document IDs, employee names and credential IDs were removed or replaced with placeholders (`YOUR_...`). Import into n8n and connect your own accounts to run them.

## 1. Contract generator (Telegram bot)

A Telegram bot that collects contract details in a dialog and produces a ready contract in minutes.

| File | What it does |
|---|---|
| `01_telegram_bot_menu_and_dialog.json` | Telegram menu and dialog, session handling, LLM-based extraction of company details from text/photos (OCR + OpenAI), input validation |
| `02_contract_generation.json` | Copies a Google Docs template, replaces variables via Google Docs API, exports DOCX/PDF through Drive API, sends the file to the chat and clears the session |
| `03_bitrix_task_and_sheet_log.json` | Logs the contract to Google Sheets and creates a task in Bitrix24 via REST API |
| `contract_generator_single_workflow.json` | Earlier single-workflow version of the same system |

**Flow:** Telegram dialog → validation → Google Docs template copy and variable replacement → export → send to chat → log to Sheets → Bitrix24 task.

## 2. Blog publishing pipeline

| File | What it does |
|---|---|
| `blog_publishing_pipeline.json` | Scheduled pipeline: reads topics from NocoDB, generates long-form articles and HTML with Gemini, builds structured data, publishes to WordPress by category and updates the status in NocoDB |

## Setup

1. Import a JSON file into n8n.
2. Create credentials (Telegram, Google, OpenAI, Bitrix24 webhook, WordPress, NocoDB, Gemini) and select them in the nodes.
3. Replace placeholders: `YOUR_TEMPLATE_01_DOC_ID`, `YOUR_TEMPLATE_02_DOC_ID`, `YOUR_GOOGLE_SHEET_ID`, `YOUR-PORTAL.bitrix24.com`, `YOUR_WEBHOOK_TOKEN`, `YOUR_OCR_SPACE_API_KEY`, NocoDB IDs.
4. Create Google Docs templates with `{{variables}}` matching those in the replacement node.
