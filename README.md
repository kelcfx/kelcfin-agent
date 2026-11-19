# KELCfin Agent

**A Telegram-controlled AI assistant powered by Cloudflare Workers and Google Gemini.**

KELCfin Agent is a serverless AI assistant designed to help with research, information retrieval, browser-based tasks, programming, and general productivity through Telegram.

The project uses Cloudflare Workers as its execution environment and integrates AI models and external services to extend its capabilities.

## Project Overview

KELCfin Agent provides a conversational interface through Telegram, allowing its authorized owner to interact with an AI assistant without needing to access the underlying Cloudflare Worker directly.

The agent uses an adaptive model-routing approach to select between fast and more capable AI models, depending on the task.

## Features

- **Telegram Integration:** Interact with the assistant through Telegram commands and messages.
- **Adaptive AI Routing:** Routes requests between fast and smart Gemini models.
- **Web Research:** Uses Tavily to search for relevant online information.
- **Browser Automation:** Integrates Browserless for browser-based navigation and interaction.
- **Browser Planning:** Uses AI-generated plans to guide supported browser actions.
- **Verified Form Interaction:** Supports browser form interaction with action verification.
- **Conversation Memory:** Uses Cloudflare KV to retain conversation context.
- **Owner Authorization:** Restricts access to authorized Telegram users.
- **Command Interface:** Provides dedicated commands for research, browsing, model selection, and agent management.
- **Serverless Deployment:** Runs on Cloudflare Workers without requiring a dedicated VPS.

## Technology Stack

| Technology | Purpose |
|---|---|
| JavaScript | Application logic |
| Cloudflare Workers | Serverless execution environment |
| Cloudflare KV | Conversation and application state |
| Telegram Bot API | User interaction |
| Google Gemini | AI reasoning and responses |
| Tavily | Web search and research |
| Browserless | Browser automation |

## Architecture

```text
Telegram User
      |
      v
Telegram Bot API
      |
      v
Cloudflare Worker
      |
      +---- Google Gemini
      |       |
      |       +---- Fast Model
      |       +---- Smart Model
      |
      +---- Tavily Web Research
      |
      +---- Browserless
      |       |
      |       +---- Browser Navigation
      |       +---- Page Interaction
      |       +---- Form Interaction
      |
      +---- Cloudflare KV
              |
              +---- Conversation Memory
              +---- Application State
```

## Available Commands

The agent supports the following Telegram commands:

| Command | Description |
|---|---|
| `/start` | Start interacting with the bot |
| `/help` | Display available commands |
| `/status` | Display agent status and configuration |
| `/agent` | Access agent functionality |
| `/browse` | Start a browser-related task |
| `/click` | Perform a supported browser click action |
| `/type` | Enter text into a supported browser field |
| `/browser` | Access browser controls |
| `/search` | Search for information |
| `/research` | Perform web research |
| `/read` | Retrieve and read webpage content |
| `/fast` | Select fast AI response mode |
| `/smart` | Select smart AI response mode |
| `/auto` | Enable automatic model routing |
| `/reset` | Reset conversation context |

*Command availability and behavior depend on the deployed Worker configuration.*

## Deployment

KELCfin Agent is designed to run on Cloudflare Workers.

### Requirements

Before deploying, you will need:

- A Cloudflare account.
- A Telegram bot created through BotFather.
- A Google Gemini API key.
- A Tavily API key.
- A Browserless API key.
- A Cloudflare KV namespace.

### Environment Variables

Configure the following environment variables in your Cloudflare Worker settings:

| Variable | Purpose |
|---|---|
| `TELEGRAM_BOT_TOKEN` | Telegram bot authentication |
| `TELEGRAM_WEBHOOK_SECRET` | Telegram webhook verification |
| `TELEGRAM_OWNER_ID` | Authorized Telegram user ID |
| `GEMINI_API_KEY` | Google Gemini API access |
| `TAVILY_API_KEY` | Tavily search access |
| `BROWSERLESS_API_KEY` | Browserless API access |

### Cloudflare KV Binding

Create a Cloudflare KV namespace and bind it to the Worker using the binding name:

`STATE`

The application uses this binding for conversation memory and application state.

### Deployment Steps

1. Create a Cloudflare account.
2. Create a new Cloudflare Worker.
3. Add the project source code.
4. Create the required KV namespace.
5. Configure the `STATE` KV binding.
6. Add the required environment variables and secrets.
7. Deploy the Worker.
8. Configure the Telegram webhook to point to the Worker’s Telegram endpoint.
9. Test the bot through Telegram.

## Worker Endpoints

| Endpoint | Purpose |
|---|---|
| `/` | Main application endpoint |
| `/health` | Health check |
| `/setup` | Setup endpoint |
| `/telegram` | Telegram webhook endpoint |

## Configuration

The current source configuration uses:

- Fast model: `gemini-3.5-flash-lite`
- Smart model: `gemini-3.8-flash`
- Automatic model routing
- Maximum agent rounds: 3
- Maximum agent actions: 4
- Browser operation timeout: 25 seconds
- Model response timeout: 12 seconds
- Telegram message limit: 3,900 characters
- Conversation history limit: 10 messages

These are application configuration values and may be adjusted as the project develops.

## Security

Security is an important consideration in the design and deployment of KELCfin Agent.

The project incorporates:

- Telegram owner authorization.
- Webhook secret verification.
- Environment-based credential management.
- Browser URL validation.
- Browser action validation against available page information.
- Duplicate Telegram update protection.
- Conversation state management.

**Important:** Never publish API keys, bot tokens, webhook secrets, or other private credentials in a public repository. Store sensitive values in Cloudflare Worker environment variables and secrets.

Browser automation should be used responsibly. Review actions before allowing automation to interact with sensitive accounts, submit important forms, or perform consequential operations.

## Project Status

**Version:** 2.7.2

**Deployment Platform:** Cloudflare Workers

**Interface:** Telegram

**Project Type:** Personal AI Assistant

The repository contains the application source code for the KELCfin Agent project. Features and integrations may evolve as development continues.

## Repository

GitHub: https://github.com/kelcfx/kelcfin-agent

## Author

**KELCfin**

An independent project focused on building practical AI-powered tools and automation workflows.

---

*Built with JavaScript, Cloudflare Workers, Google Gemini, Telegram, Tavily, and Browserless.*
