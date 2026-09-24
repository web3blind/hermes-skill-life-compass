# Life Compass / Компас жизни

A portable [Hermes Agent](https://hermes-agent.nousresearch.com/docs/) skill for gentle life orientation **and** an optional rhythm of user-chosen directions. No fixed life plan is installed. Installing the skill does not schedule anything.

**This is not [Gentle Planning](https://github.com/web3blind/hermes-skill-gentle-planning).** Gentle Planning helps build day/week/month and work-session plans. Life Compass does not require a plan: it helps notice what matters, make a small calm choice, and — only if requested — use gentle reminders and optional feedback to tune a rhythm.

## Возможности

- Разговорный «компас»: отличать реальную задачу от внутренней гонки; выбирать небольшой шаг, паузу или отказ без самонаказания.
- Пять выбранных человеком направлений — удобный пример, но не ограничение: число, дни и часы задаёт сам человек. Напоминания включаются только с согласия.
- Необязательная обратная связь 0–5 о нужности и цене действия. `0` — не требовалось или сделано заранее; `4` — сделал, но раздражало; `5` — сегодня не сделал (причина неизвестна). Пропущенный ответ ничего не означает.
- Короткий недельный обзор только по доступной истории, без оценок человека и без обязательного отчёта.
- По запросу — лёгкое планирование, пауза перед сном, отдельные календарные напоминания о событиях с конкретным временем.

## Install / установка

```bash
git clone https://github.com/web3blind/hermes-skill-life-compass.git ~/.hermes/skills/life-compass
```

Or copy the entire directory, including `SKILL.md` and `references/`, into a folder your agent uses for skills. `references/` is required for the full workflows. Confirm your particular installation's skill search path. No private data or working schedules should go inside the cloned repository.

## Start / начало

Try: `Help me use Life Compass in conversation-only mode; no reminders.`

For reminders: `Help me choose five directions and show a schedule draft. Ask before creating any job.`

For a review: `Review the last seven days using only the history you can actually access. If you cannot read it, say so.`

Example private data shape: [`examples/compass.example.json`](examples/compass.example.json). Copy it to your own private location if you want to retain settings. It is empty and **not** loaded or scheduled automatically. See [`references/setup.md`](references/setup.md) for consent, scheduling, and verification. A Telegram bot's numeric replies are plain text unless its delivery path explicitly supports buttons.

## Boundaries

Not therapy, diagnosis, a financial advisor, or an autonomous life manager. No compulsory month/week/day cascade, no streaks, no public diary. A calendar event or reminder never authorizes payments or public actions. The repository contains no real user's directions, chat IDs, schedules, feedback, or access credentials. License: MIT.
