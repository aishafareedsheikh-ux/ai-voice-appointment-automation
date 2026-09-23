# Outbound Dental Recall Calling Agent

An automated outbound calling system that combines Make.com, Airtable, and Vapi to call patients due for recall/follow-up appointments — no manual dialing needed.

## How it works
1. **Airtable (Search Records)** – Runs on a daily schedule (9:00 AM) to pull patient records due for a recall call.
2. **HTTP (POST /call/phone)** – Sends each patient's details to a Vapi endpoint, which triggers an outbound call from the AI voice agent.
3. **Airtable (Upsert a Record)** – Updates the record afterward to mark the call as attempted, so the same patient isn't called twice.

## AI Voice Agent — "Sophie: Dental Recall Agent"
Built on Vapi, this agent handles the actual phone conversation:
- **Transcriber:** Deepgram Flux (English)
- **Model:** GPT-4o Mini Cluster
- **Voice:** Vapi "Clara"
- **Opening line:** `Hi, is this {{customer.name}}?`

## Tech stack
- **Make.com** – scheduling, orchestration, Airtable ↔ Vapi bridge
- **Airtable** – patient/appointment database
- **Vapi** – AI voice agent (STT: Deepgram, LLM: GPT-4o Mini, TTS: Vapi Clara)
