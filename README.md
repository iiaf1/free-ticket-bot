# 🎫 Free Ticket Bot — Discord Ticket System

A complete Discord ticket bot built with **discord.js v14**, fully powered by **Slash Commands**, with **multi-category ticket support**, ticket claiming, automatic DM reminders, and full **HTML transcript logging**.

## ✨ Features

- Fully slash-command driven: `/setup-tickets`, `/add-ticket-type`, `/remove-ticket-type`, `/list-ticket-types`, `/send-panel`, `/close`, `/add`, `/remove`, `/claim`.
- **Multiple ticket categories/types** (e.g. Inquiry, Bug Report, Complaint) — each with its own channel category and support role.
- A dropdown select-menu panel (instead of a single button) listing every configured ticket type.
- Close button with a confirmation prompt.
- **`/claim` command** — support staff can claim a ticket, notifying the opener right in the channel.
- **Automatic DM follow-up reminder** — if support replies and the ticket opener doesn't respond within 5 minutes, the bot DMs them a reminder with a direct link back to the ticket.
- Private ticket channels with correctly scoped permissions (opener + the relevant support role only).
- Prevents a member from opening more than one ticket of the same type at once.
- Generates a **full HTML transcript** (messages, attachments, images, embeds, ticket type, claimed-by) sent to your log channel on close.
- Per-guild settings stored in `data/settings.json` — no external database required.
- Automatic channel cleanup after a ticket is closed.

## 📦 Installation

```bash
npm install
```

## ⚙️ Configuration

1. Copy `.env.example` to a new file named `.env`.
2. Fill in the following values:
   - `TOKEN`: your bot token from the [Discord Developer Portal](https://discord.com/developers/applications).
   - `CLIENT_ID`: your application's Client ID.
   - `GUILD_ID`: (optional) your server ID, for instant command registration during development. Leave empty for global registration.
3. When inviting the bot, make sure it has these permissions:
   - `Manage Channels`
   - `View Channels`
   - `Send Messages`
   - `Read Message History`
   - `Attach Files`
   - `Embed Links`
4. Enable these Privileged Gateway Intents in the Developer Portal → Bot:
   - `Server Members Intent`
   - `Message Content Intent`

## 🚀 Running the Bot

First, register the slash commands:

```bash
npm run deploy
```

Then start the bot:

```bash
npm start
```

## 🧭 Usage Guide

1. `/setup-tickets` — set the log channel that will receive closed-ticket transcripts.
2. `/add-ticket-type` — add each ticket type you want (e.g. Inquiry, Bug Report), specifying:
   - The category channels for that type will be created under.
   - The support role responsible for that type.
   - An optional description and emoji.
   - Repeat for every type you need (up to 25).
3. `/list-ticket-types` to review current types, and `/remove-ticket-type` to delete one.
4. `/send-panel` — send the ticket panel (dropdown menu) in the desired channel. Re-run it after editing your ticket types to refresh the panel.
5. Any member selecting a type from the menu gets their own private channel configured for that type.
6. Inside a ticket channel:
   - `/add` — add a member to the ticket.
   - `/remove` — remove a member from the ticket.
   - `/claim` — support staff claim the ticket (posts a confirmation message and notifies the opener).
   - `/close` or the **"Close Ticket"** button — closes the ticket and saves its transcript.
7. **Automatic reminder**: any message from a support-role member in a ticket channel starts a 5-minute timer. If the opener hasn't replied by then, they get a DM reminder. Replying, or the ticket being closed, cancels the reminder.

## 📁 Project Structure

```
free-ticket-bot/
├── commands/            # Slash commands
│   ├── setup-tickets.js
│   ├── add-ticket-type.js
│   ├── remove-ticket-type.js
│   ├── list-ticket-types.js
│   ├── send-panel.js
│   ├── close.js
│   ├── add.js
│   ├── remove.js
│   └── claim.js
├── events/              # Discord.js event handlers
│   ├── ready.js
│   ├── interactionCreate.js
│   └── messageCreate.js
├── utils/                # Helpers
│   ├── db.js
│   ├── ticketManager.js
│   ├── transcript.js
│   └── reminderTracker.js
├── data/                # Auto-generated (per-guild settings)
├── transcripts/           # Auto-generated (local transcript copies)
├── index.js
├── deploy-commands.js
├── package.json
├── .env.example
└── LICENSE.md
```

## 📜 License

This project is licensed under the **MIT License** — see [LICENSE.md](./LICENSE.md) for the full text.

Copyright (c) 2026 **iaf0**. All rights reserved.

## 📬 Contact & Support

Questions, bug reports, or want to contribute? Reach out:

- 💬 **Discord:** `iaf0`
- 🐙 **GitHub:** [github.com/iiaf1](https://github.com/iiaf1)

Feel free to open an issue on GitHub or DM me on Discord for support.
