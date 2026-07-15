**You:**
Build an inbound voice agent for a business that qualifies leads on phone calls. The agent should:
1. Greet the caller warmly and ask how it can help
2. Ask for their name
3. Ask what service they're interested in
4. Ask their budget range or urgency
5. Ask their preferred contact time
6. Thank them and confirm someone will follow up soon
Keep responses short and natural like a real phone conversation. At the end of the call, trigger a function/tool call that sends the collected data (name, service, budget, preferred time) to an external webhook.

---

**Composer:**


---

**Composer:**


---

**Composer:**


---

**Composer:**


---

**Composer:**
I created the **webhook tool** already, but assistant creation failed because your org **doesn’t have access to the Vapi transcriber** (`400: Vapi transcriber is not available for your organization.`).

## What I already created
- **Tool**: `send_lead_to_webhook`  
  **Tool ID**: `1761a019-e876-4fdf-b1a6-65a48f9250e0`

## Next step (so I can finish the inbound agent)
Which **transcriber provider** do you want to use instead (e.g., `deepgram`, `assembly-ai`, `openai`, `gladia`)?

---

**You:**
deepgram

---

**Composer:**


---

**Composer:**
Assistant creation failed again—your org also **doesn’t have access to the Vapi model** (`400: Vapi model is not available for your organization.`). The **Deepgram** transcriber choice is fine.

To finish building the inbound lead-qualifier agent, which **LLM provider/model** do you want to use instead?

- **OpenAI** (e.g. `gpt-4o-mini` or `gpt-4o`)
- **Anthropic** (e.g. `claude-3-5-sonnet`)
- **Groq** (fast, e.g. `llama-3.1-70b-versatile`)
- Or tell me what you have credentials for

---

**You:**
google gemini, gemini-2.5-flash

---

**Composer:**


---

**Composer:**


---

**Composer:**
## Built ✅
Your inbound lead-qualifier assistant is created.

- **Assistant**: *Inbound Lead Qualifier*  
  **Assistant ID**: `cdde57ff-73e1-4784-87e3-7b74beeae289`
- **Transcriber**: Deepgram `nova-2`
- **Model**: Google `gemini-2.5-flash`
- **Voice**: Vapi `Elliot` (v2)
- **Tool (created earlier)**: `send_lead_to_webhook`  
  **Tool ID**: `1761a019-e876-4fdf-b1a6-65a48f9250e0`

## Test it now (web call)
I started a dashboard test call for this assistant — use the **test call card** to talk to it.

## One missing piece: your webhook URL
Right now the tool exists, but it **isn’t pointed at your external webhook** yet (no `server.url` configured), so it can’t actually send the data out.

What’s the **webhook URL** you want `send_lead_to_webhook` to call?

---

**You:**
https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf

---

**Composer:**


---

**Composer:**
I’m ready to connect your tool to n8n by setting `send_lead_to_webhook.server.url` to:

`https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`

Please click **Approve** on the update card to apply this change.

---

**Composer:**
✅ Done — your tool is now connected to n8n.

- **Tool** `send_lead_to_webhook` (`1761a019-e876-4fdf-b1a6-65a48f9250e0`)
- **Webhook**: `https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`
- **Timeout**: `20s`

## What to test
1. Place a test call to **Inbound Lead Qualifier** (`cdde57ff-73e1-4784-87e3-7b74beeae289`).
2. Answer the questions (name, service, budget/urgency, preferred time).
3. At the end, it should say it’s passing it along, then your **n8n workflow should receive a POST** with those fields.

When you’ve done a test call, paste the **call ID** here and I’ll pull the transcript + tool-call details to confirm the webhook fired and what payload was sent.

---

**You:**
Update the send_lead_to_webhook tool's server URL to: [https://ali04.app.n8n.cloud/webhook-test/d3c32531-c9a8-4b53-82ef-fe35b208bfbf]

---

**Composer:**


---

**Composer:**
I’ve queued the update to point `send_lead_to_webhook` at:

`https://ali04.app.n8n.cloud/webhook-test/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`

Please click **Approve** on the update card to apply it.

---

**Composer:**
✅ Confirmed — `send_lead_to_webhook` is now pointing to your **n8n test webhook**:

- **Tool**: `send_lead_to_webhook` (`1761a019-e876-4fdf-b1a6-65a48f9250e0`)
- **server.url**: `https://ali04.app.n8n.cloud/webhook-test/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`
- **timeoutSeconds**: `20`

If you place a quick test call to the assistant now, n8n should receive the lead payload at the end of the conversation.

---

**You:**
Update the send_lead_to_webhook tool's server URL back to: [https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf]

---

**Composer:**


---

**Composer:**
I’ve queued the revert to point `send_lead_to_webhook` back to:

`https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`

Please click **Approve** on the update card to apply it.

---

**Composer:**
✅ All set — the `send_lead_to_webhook` tool is now reverted back to your **production** n8n webhook:

- **Tool**: `send_lead_to_webhook` (`1761a019-e876-4fdf-b1a6-65a48f9250e0`)
- **server.url**: `https://ali04.app.n8n.cloud/webhook/d3c32531-c9a8-4b53-82ef-fe35b208bfbf`
- **timeoutSeconds**: `20`

If you run one more quick test call, it should POST the lead payload to that production endpoint at the end of the conversation. After you hang up, send me the **call ID** and I’ll confirm the tool fired (and whether the webhook returned a success).