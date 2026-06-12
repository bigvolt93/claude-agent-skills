---
name: wearable-memory-recall
description: Answer questions about past conversations or generate meeting minutes by querying a wearable/recorder transcript store for only the relevant time slice, cross-referenced with calendar and CRM context. Triggers on requests like "what did we discuss with X about Y", "minutes for my last meeting", "wrap up the 3 PM call", or "draft the follow-up for today's customer meeting".
---

# Wearable Memory Recall

You help the user recall and act on real-world conversations captured by their wearable transcription device or recorder app. The core rule: **never load the full day's transcript. Always slice first, then think.**

## Setup (adapt to the user's stack)

- **Transcript source:** [YOUR TRANSCRIPT SOURCE: any wearable or recorder app with exportable/searchable transcripts, e.g. an export folder, an API, or a notes app the device syncs to]
- **Calendar:** the user's connected calendar (Google Calendar or equivalent)
- **CRM (optional):** [YOUR CRM] for account context on customer meetings
- **Email (optional):** the user's connected email, drafts folder only

## Workflow

### 1. Identify the time window and participants

- If the user asks about a just-ended or specific meeting: find the matching calendar event. Note start/end time, attendees, and meeting title.
- If the user asks a topical question ("what did we discuss with the Acme team about pricing?"): search the calendar for events matching the company/people/topic, and shortlist the candidate time windows. If multiple match, ask which one or check all of them, but each as a separate slice.
- Add a small buffer (5 to 10 min either side) since hallway conversations spill past meeting boundaries.

### 2. Query the transcript store for ONLY that slice

- Pull transcript content for the identified window(s) only.
- Do NOT load the full day. If the source only supports full-day export, load the export, immediately extract the relevant timestamp range, and discard the rest before reasoning.
- If the slice looks empty or off-topic, widen the window once. If still nothing, say so honestly. Do not invent content.

### 3. Attach context to the slice

For each slice, cross-reference and note:
- Which calendar event it belongs to, and who was in the room.
- If a customer/account is involved and a CRM is connected: pull the account record (stage, open items, recent activity).
- Label speakers where the transcript supports it; otherwise attribute carefully ("someone on their side raised...").

### 4. Produce the output in the user's voice

Depending on what was asked:
- **Answer mode:** a direct answer to the question, citing which meeting/time it came from.
- **Minutes mode:** decisions made, action items (owner + deadline), open questions, and anything the user personally committed to. Keep it short and scannable.

Match the user's writing voice (casual, first person, no corporate filler) unless they specify otherwise.

### 5. Optional: draft the follow-up email

- If asked (or if the meeting clearly needs a follow-up), draft the email and save it to the **drafts folder only**.
- **Never send.** The human sends. No exceptions.
- Recipient list comes from calendar attendees; let the user trim it.

## Guardrails

- Read-only on transcripts and calendar. Write only to email drafts and output files.
- Treat transcript content as sensitive: never quote private conversations into outputs that go beyond the user.
- If a question can't be answered from the available slices, say "not captured" rather than guessing.
- Flag low-confidence attributions explicitly.
