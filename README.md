# UPSC/BPSC Mains Answer Evaluator

An n8n Telegram workflow that reads a handwritten answer photo and returns a practice score and actionable feedback.

[Try the Telegram bot](https://t.me/mamsheetevaluationbot)

## Features

- Accepts one Telegram photo with the exam question in its caption.
- Downloads the photo and checks that the image and question are present before calling AI.
- Uses one image-capable model call for handwriting reading, analysis, scoring and improvement advice.
- Returns a score out of 10, reasons for deductions, strengths, actionable improvements and suggested value additions.
- Sends upload instructions for missing photos or captions.
- Extracts model feedback from the content blocks and escapes Telegram HTML characters.

## Workflow

Telegram Trigger -> Photo And Question Present? -> Evaluate Answer Sheet -> Send Feedback to Student

The false branch sends upload instructions.

## Setup

1. Import `workflow.json` into n8n.
2. Create a Telegram bot through BotFather and connect its credential to the trigger and both send nodes. Use a separate bot for each active Telegram workflow.
3. Connect an OpenAI credential or supported n8n AI Gateway connection to the evaluation node. Confirm that `gpt-4o-mini` image analysis is available in your account.
4. Keep photo download enabled on the trigger. The evaluator expects binary image data, not only a Telegram file ID.
5. Execute the workflow for a test, then send ONE clear photo using Telegram's photo upload, with the complete question in the photo caption. Documents and question messages sent separately are rejected.
6. Check the feedback, then publish for automatic message-triggered runs.

## Cost controls

The workflow uses a single evaluation call instead of separate OCR, analysis, scoring and mentor calls. Output is capped at 700 tokens and the prompt requests concise feedback. Missing-photo or missing-question inputs are rejected before evaluation. Actual cost depends on the image, model and provider pricing.

## Validation and limitations

A real answer photo was evaluated in the original configured workflow. The corrected feedback send step was verified using that saved evaluation output and accepted by Telegram without repeating the AI call. A fresh full execution after that correction was not independently verified in this export-preparation session.

Scores are approximate practice feedback, not official UPSC/BPSC marks. Handwriting quality and image clarity affect results. Suggested facts and value additions should be checked against reliable sources. Only one photo is supported per evaluation; multi-page documents are not handled by this workflow.

Photos and captions are processed by your configured model provider and may appear in n8n execution history. Avoid sending unnecessary personal information. Demo availability depends on the owner's hosting and model credits.

## Export contents

Credential references, pinned execution data and instance/workflow metadata have been removed. This export is inactive; reconnect credentials and test before publishing. No bot tokens are included.
