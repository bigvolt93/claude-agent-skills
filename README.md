# Claude Agent Skills

Skills from my personal agent fleet, the one behind the ["Building Cool Agents with AI"](https://sagaofthakar.substack.com) series. Eight agents I run every day on Claude Cowork, sanitized and packaged so you can adapt them.

I'm not a developer. I run P&Ls. Everything here was built with prompts, open-source parts, and jugaad. If I can wire this up, you can.

## The skills

| Skill | What it does | Blog post |
|---|---|---|
| [whatsapp-cowork-connection](whatsapp-cowork-connection/) | Starter skill for a WhatsApp-connected assistant: daily unreads digest, never sends without approval | [blog](https://sagaofthakar.substack.com/p/whatsapp-claude-jugaad) |
| [gobabygo-summon-bot](gobabygo-summon-bot/) | A summon-style agent that lives in your team WhatsApp group. Tag it with a task, it picks it up on the next tick | [blog](https://sagaofthakar.substack.com/p/gobabygo-summon-bot) |
| [family-food-tracker](family-food-tracker/) | 24/7 family nutritionist in a WhatsApp group. Photo in, calorie and macro recap out, 3x a day | [blog](https://sagaofthakar.substack.com/p/family-food-tracker-whatsapp) |
| [meeting-wrap-up](meeting-wrap-up/) | Calendar to CRM sync: transcripts, email context, dedupe by event ID, leads created only on ICP fit | [blog](https://sagaofthakar.substack.com/p/my-meetings-file-themselves) |
| [accountability-nudge](accountability-nudge/) | Twice-daily open-task nudge from your CRM to your team group chat. ~30 lines, runs on the cheapest model | [blog](https://sagaofthakar.substack.com/p/cheapest-agent-highest-roi) |
| [followup-monitor](followup-monitor/) | Detects prospect replies, drafts cadence-based follow-ups for human approval. Never auto-sends | [blog](https://sagaofthakar.substack.com/p/followup-monitor-agent) |
| [neosapien-agent-memory](neosapien-agent-memory/) | Query a wearable's transcript memory for the relevant slice instead of dumping 8 hours of audio | [blog](https://sagaofthakar.substack.com/p/i-gave-my-agent-ears) |
| [resume-linkedin-sync](resume-linkedin-sync/) | Diffs your resume against your LinkedIn profile, reports inconsistencies, drafts aligned copy | [blog](https://sagaofthakar.substack.com/p/resume-linkedin-sync-agent) |

## How to use

1. Open Claude Cowork (or Claude Code) and add the skill folder you want.
2. Replace the placeholders: `YOUR_GROUP_JID`, `YOUR_WEBHOOK_URL`, `YOUR_STATUS_ID`, and friends.
3. WhatsApp-based skills need a local bridge (the open-source whatsapp-mcp pattern). The first blog post walks through it.
4. Schedule the ones meant to run on their own. Start with one. Keep it alive for a month.

## Ground rules these skills follow

State lives outside the agent. Idempotency everywhere. Log after success, not before. Append-only writes with backups. Drafts for humans, never auto-send where a relationship is involved. Caps per run. These rules are why the fleet has survived thousands of runs.

## License

MIT. Take it, adapt it, ship it. A mention is appreciated, not required.

---

Built by [Sagar Thakar](https://linkedin.com/in/sagarthakar). Operator at ClearTax, founding team ClearTax.ai. Disclosure: I'm an angel investor in Neosapien, the wearable referenced in one skill.
