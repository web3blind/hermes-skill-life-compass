# Consent-based setup and portable automation

The skill works as a conversation **without** any integration. Do not create reminder jobs just because the skill was installed.

## Interactive setup

1. Ask whether the person wants conversation-only mode, reminders, optional feedback history, weekly review, and/or calendar reminders. These are separate opt-ins.
2. Ask for their own direction names (five is the example shape), cadence and local times, time zone, delivery destination, quiet hours, and whether feedback should be shown after each reminder. Accept directions without any reminder.
3. Show a compact proposed schedule and example message before creating it. Review notification volume and duplicates with existing calendars or other agents.
4. On explicit approval, use the platform's supported scheduler and messaging tools. Keep a reversible list of the created job IDs in **user-owned private state**, not in this repository. Validate each target and next run. A test delivery is separate and should be requested when it posts to a real chat.
5. Offer pause, edit, and removal. Delete only user-requested jobs; do not remove unrelated jobs or transcripts. Sensitive/financial actions require separate confirmation.

### Hermes Agent example (adapt, do not run blindly)

Check the installed version's `hermes cron create --help` first. Example of one *agent* reminder, **only after** a user has approved the time and destination:

```bash
hermes cron create '0 9 * * 1-5' 'Use life-compass. User-approved direction: <replace-with-direction>. Offer this optional step: <replace-with-step>. Do not invent another task or demand feedback.' --name life-compass-direction-1 --deliver telegram
```

This expression is interpreted in the scheduler's configured time zone; verify the actual `next_run_at` before claiming a local 09:00 reminder. A fixed UTC cron and a named local time may diverge during daylight-saving transitions. Use explicit destinations for multi-chat setups; `telegram` may mean a home channel, not the current topic. Never hardcode another person's chat or thread IDs. Cron text alone does not imply Telegram inline buttons or access to the user's private feedback store.

A weekly review agent job needs read access to the user's approved **specific conversation/source** and an instruction to apply [review.md](review.md) to the exact preceding seven days. Set `history_source` in private config before enabling it; verify coverage and avoid unrelated chats. Do not create it when history is inaccessible; do not replace missing history with reminders or invented achievements. A no-agent/script-only job may deliver a static reminder but cannot reason over history on its own.

## Private state (optional)

The distributable `examples/compass.example.json` has placeholders and empty logs. Copy it to a private user-controlled workspace and fill it in there if needed. It is **not** a live config, and this repository must never receive a populated copy. Keep only necessary data (direction IDs, approved schedule and destination, created job IDs, optional feedback records, last verified review window). Restrict filesystem permissions according to the environment, avoid recording full chat transcripts, and support deletion/export on request. An assistant without state persistence must say it cannot reliably track trends across sessions.

## Verification checklist

- The reminder came from explicit opt-in and reflects user-defined directions; no prefilled life goals.
- Correct scheduler, timezone and next actual run; separate weekday/weekend behavior as chosen.
- Correct destination/profile/topic; test one real delivery only with permission.
- Optional numeric reply is mapped to the correct reminder, with 0 and 5 interpreted exactly; silence stays unknown.
- The weekly review uses accessible actual history or explicitly states its limits.
- No secret, personal state, or delivery ID is present in the installed public skill tree.
- All new jobs can be paused or removed individually.
