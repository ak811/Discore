# Infinity Bot

A large-scale, modular Discord community platform built with **Python** and **discord.py**, comprising approximately **300 modules** and **72 plugin extensions**.

Infinity Bot powers community operations, engagement systems, progression, virtual economy mechanics, social games, voice utilities, AI-powered features, and administrative tooling within an extensible architecture designed for a large Discord community.

The platform is primarily designed for a configured Discord guild, with fast guild-scoped application-command synchronization during development.

## Overview

Infinity Bot serves as the central automation and application layer for a large Discord community.

At its current scale, the codebase consists of approximately:

- **~300 modules**
- **72 plugin extensions**
- Multiple feature domains spanning community operations, engagement, economy, games, AI, voice, networking, onboarding, statistics, and administration

Its feature set includes:

- Server navigation and member utilities
- XP, progression, streaks, and leaderboards
- Multi-currency economy and shop systems
- AI-powered personas and quiz generation
- Social and minigame systems
- Voice-state tracking and transcription infrastructure
- Administrative and moderation utilities
- Backup, permission-audit, and maintenance tooling
- Custom Discord interactions through commands, components, embeds, reactions, and webhooks

The modular extension architecture allows individual systems to be developed, loaded, maintained, and expanded independently instead of concentrating hundreds of features inside a monolithic bot implementation.

## Platform Scale

Infinity Bot is designed as a **large Discord community platform**, rather than a small collection of commands.

```text
Infinity Bot
├── ~300 Python/application modules
├── 72 plugin extensions
├── Prefix command system
├── Discord application commands
├── Event-driven listeners
├── AI integrations
├── Economy and progression systems
├── Games and social systems
├── Voice infrastructure
├── Administrative tooling
└── Community automation
```

Individual extensions can encapsulate:

- Prefix and application commands
- Event listeners
- Background tasks
- Discord UI components
- Database and state operations
- External API integrations
- Feature-specific configuration
- Permission and authorization logic

This structure allows features to evolve independently while sharing a common Discord runtime.

## Features

### Community and Server Utilities

Infinity Bot includes utilities intended to make server information and navigation easier for members, including:

- Custom `!help` command
- FAQ interfaces and panels
- Server command directory
- Quick-guide embeds
- Role and channel information
- Community perk documentation
- Member-facing Discord utilities
- Automatic reactions
- Direct-message utilities
- Birthday-related functionality

These systems provide a programmable alternative to maintaining repetitive server documentation and common responses manually.

### Engagement and Retention

#### Daily streaks

Member activity can contribute toward daily streak progression. Supported activity sources include:

- Sending messages
- Adding reactions
- Joining voice channels
- Switching voice channels

The streak system can integrate with other progression and reward mechanics.

#### XP and progression

Infinity Bot includes XP-based progression features such as:

- XP accumulation
- Role progression ladders
- Member profiles
- Leaderboards
- Activity-based progression

Role rewards can be tied to Discord roles where the bot has sufficient permissions and role hierarchy access.

### AI Personas

Infinity Bot can expose AI-backed Discord personas that respond to members when mentioned directly or replied to through an associated message.

Responses can be sent through Discord webhooks, allowing personas to appear with distinct names, avatars, character identities, and response behavior. Persona generation uses the OpenAI API and requires a valid `OPENAI_API_KEY` plus appropriate Discord webhook permissions.

### AI Quiz Generation

The quiz system can use OpenAI models to generate questions programmatically. Depending on installed optional dependencies and configuration, source material can include:

- PDF
- DOCX
- PPTX
- XLSX

The asynchronous OpenAI client is used for quiz-generation workflows. Document-parsing dependencies are optional when document-backed quiz generation is not required.

## Economy

Infinity Bot implements a multi-layer virtual economy:

```text
Coins → Orbs → Stars → Diamonds
```

Different currencies can represent different levels of value or progression inside the community economy.

Economy functionality includes:

- Member balances
- Currency transfers
- Currency conversion and exchange mechanics
- Shop purchases
- Collectibles
- Custom role purchases
- Subscription-style rewards
- Progression rewards
- Economy utilities

Example commands include:

```text
!coins
!send_coins
!diamonds
```

The exact command set depends on the enabled economy extensions.

### Shop System

The shop provides an extensible mechanism for exchanging virtual currency for server rewards. Depending on configuration, shop items can include:

- Collectibles
- Custom roles
- Subscription-style perks
- Currency exchanges
- Community rewards
- Other configurable virtual products

The shop works alongside the XP and currency systems as part of the broader progression loop.

## Games and Social Systems

Infinity Bot contains a variety of lightweight social and game-oriented modules, including:

- Clans
- Spin wheel
- Dice
- Fortune
- Topic prompts
- Betting
- Nickname helper
- Word Snake
- Tree minigame
- Other community games and interaction systems

Individual features are separated into their relevant extensions and modules to keep game logic independent from core startup and server-management functionality.

## Voice Features

### Voice-State Tracking

Infinity Bot listens to Discord voice-state changes and can use them for:

- Activity tracking
- Streak progression
- Join and leave detection
- Channel-switch detection
- Other voice-related automations

### Voice-Message Transcription

The repository contains infrastructure for voice-message transcription, including a **no-op speech-to-text fallback**. This keeps the transcription interface operational even when a production STT provider has not been configured.

The backend can be replaced or extended with services such as:

- OpenAI speech-to-text
- Whisper-compatible services
- Cloud speech APIs
- Self-hosted transcription systems

without redesigning the surrounding Discord integration.

## Administrative Tooling

Infinity Bot includes server administration and maintenance utilities intended for authorized staff, including:

- Category and channel backups
- Channel restoration workflows
- Message purge ranges
- Permission audits
- Channel rename operations
- Channel movement and archive utilities
- Embed editing
- Sending and editing bot messages
- Adding and removing reactions
- Emoji tooling
- Host PC status reporting
- Other server maintenance operations

Administrative commands should be protected through Discord permissions, application checks, role checks, or equivalent authorization mechanisms appropriate to the deployment.

## Bitcoin Price Announcer

The economy and networking functionality includes a BTC price announcement utility that can expose Bitcoin pricing information inside Discord. External market-data functionality may depend on the configured provider and its availability.

## Architecture

Infinity Bot follows a modular `discord.py` architecture centered around extensions, Cogs, and reusable modules. With roughly **300 modules and 72 plugin extensions**, architectural separation prevents the runtime from becoming a monolithic application.

```text
Discord Gateway / REST API
          │
          ▼
       main.py
          ├── Application-command synchronization
          ├── Extension discovery and loading
          ├── Guild restrictions
          └── Application startup
                    │
                    ▼
                 bot.py
                    ├── Global bot instance
                    ├── Prefix configuration
                    ├── Shared runtime state
                    └── Common services
                              │
                              ▼
                    Extension Layer
                       72 plugins
                              │
              ┌───────────────┼───────────────┐
              ▼               ▼               ▼
          Commands         Events         Services
              └───────────────┼───────────────┘
                              ▼
                       ~300 modules
                              │
        ┌─────────────────────┼─────────────────────┐
        ▼                     ▼                     ▼
     Economy              Engagement              Admin
     Games                Voice                   Stats
     Server               Networking              AI
     Onboarding           Utilities               Other
```

This structure separates startup and runtime concerns from feature implementation.

## Repository Structure

The primary repository layout is conceptually organized around:

```text
.
├── bot.py
├── main.py
├── requirements.txt
├── LICENSE
├── configs/
│   └── ...
├── cogs/
│   ├── server/
│   ├── admin/
│   ├── stats/
│   ├── fun/
│   ├── economy/
│   ├── engagement/
│   ├── networking/
│   ├── voice/
│   ├── onboarding/
│   └── ...
├── modules/
│   └── ...
└── pycord/
    └── .env
```

The complete project contains approximately **300 modules** distributed across the platform and **72 loadable plugin extensions**.

### `bot.py`

Creates the shared/global Discord bot instance. The bot uses:

```python
command_prefix="!"
```

It also contains shared runtime state used by other parts of the application.

### `main.py`

The primary application entry point is responsible for:

- Bootstrapping the Discord client
- Registering startup behavior
- Loading configured extensions and plugins
- Synchronizing application commands
- Applying guild restrictions
- Starting the bot using the configured token

Run it with:

```bash
python main.py
```

### `cogs/`

Contains modular feature implementations grouped by domains such as:

```text
server
admin
stats
fun
economy
engagement
networking
voice
onboarding
```

The extension layer currently contains approximately **72 plugin extensions**. Each can encapsulate its own commands, event listeners, runtime behavior, feature state, Discord UI components, external integrations, and supporting business logic.

### Modules

Approximately **300 modules** provide reusable and domain-specific functionality underneath the plugin layer, including:

- Community systems and configuration
- Economy, engagement, and games
- Statistics and data processing
- Discord utilities
- AI integrations
- Voice functionality
- Administrative workflows
- Networking
- Shared helpers

Separating reusable logic from Discord command definitions helps reduce duplication across the extensions.

### `configs/`

Contains project configuration modules. `BOT_TOKEN` and `BOT_GUILD_ID` are consumed through:

```python
configs.config_general
```

The exact configuration-loading implementation can be adapted to the deployment environment.

## Command Model

Infinity Bot uses both traditional prefix commands and Discord application commands.

### Prefix Commands

The default prefix is `!`.

Examples:

```text
!help
!coins
!diamonds
!send_coins
```

Prefix-command functionality generally requires the **Message Content Intent**.

### Application Commands

The bot also uses `discord.py` application commands. Several commands are intentionally scoped to the configured guild using a pattern such as:

```python
@app_commands.guilds(discord.Object(id=BOT_GUILD_ID))
```

Guild-scoped commands are useful during development because changes generally become available much faster than globally registered commands. For a production multi-guild deployment, command registration and synchronization strategy should be reviewed accordingly.

## Requirements

A current Python 3 environment is required. Recommended tooling and access include:

- Python 3.x
- `venv`
- `pip`
- A Discord bot application
- Discord server access for installation and testing

Dependencies are defined in `requirements.txt` and can be installed with:

```bash
pip install -r requirements.txt
```

## Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd <repository-directory>
```

### 2. Create a Virtual Environment

Linux or macOS:

```bash
python -m venv .venv
source .venv/bin/activate
```

Windows PowerShell:

```powershell
python -m venv .venv
.venv\Scripts\Activate.ps1
```

Windows Command Prompt:

```cmd
python -m venv .venv
.venv\Scripts\activate.bat
```

### 3. Install Dependencies

```bash
python -m pip install --upgrade pip
pip install -r requirements.txt
```

## Configuration

Infinity Bot reads its core Discord configuration through `configs.config_general`.

At minimum, configure:

```env
BOT_TOKEN="your_discord_bot_token"
BOT_GUILD_ID="your_server_id"
```

AI functionality additionally requires:

```env
OPENAI_API_KEY="your_openai_api_key"
```

A complete development configuration may resemble:

```env
BOT_TOKEN="your_discord_bot_token"
BOT_GUILD_ID="123456789012345678"
OPENAI_API_KEY="your_openai_api_key"
```

The repository also contains `pycord/.env`. Use the environment-loading strategy that best matches your deployment, provided the values expected by the configuration modules are available at runtime.

### Environment Variables

| Variable | Required | Purpose |
|---|---:|---|
| `BOT_TOKEN` | Yes | Authenticates the Discord bot |
| `BOT_GUILD_ID` | Yes | Identifies the primary configured Discord guild |
| `OPENAI_API_KEY` | Feature-dependent | Enables AI personas and AI-powered quiz generation |

Do **not** commit production credentials to source control.

## Running Infinity Bot

Start the application with:

```bash
python main.py
```

During startup, the bot will:

1. Initialize the global Discord bot instance.
2. Register startup hooks and checks.
3. Load the configured plugin extensions.
4. Synchronize slash and application commands to the configured guild.
5. Authenticate with Discord using `BOT_TOKEN`.
6. Begin processing Discord gateway events and commands.

A successful startup should result in the bot connecting to Discord and exposing the enabled features in the configured server.

## Discord Intents

Features that rely on Discord gateway events require the corresponding intents to be enabled both in the Discord Developer Portal and in the application's `discord.py` configuration.

Depending on the enabled extensions, Infinity Bot may require access to:

- Guilds
- Guild members
- Messages
- Message content
- Reactions
- Voice states

Many prefix-command and message-listener features rely on the privileged **Message Content Intent**. Only enable privileged intents required by your deployment.

## Discord Permissions

Different modules require different Discord permissions.

| Permission | Example usage |
|---|---|
| Manage Roles | XP rewards, progression roles, custom roles |
| Manage Channels | Rename, archive, move, or restore channel structures |
| Manage Emojis and Stickers | Emoji management tooling |
| Manage Webhooks | AI persona messages |
| Read Message History | Statistics, games, backups, and message utilities |
| Add Reactions | Automatic reactions and interaction systems |
| Manage Messages | Purge and moderation utilities |
| Send Messages | Normal bot responses |
| Embed Links | Rich server guides and UI |
| View Channels | Access to relevant server channels |

Some administrative features may require additional permissions. The bot's highest role must also be positioned appropriately in the Discord role hierarchy for operations involving other roles.

## Guild Restriction

The current application is designed around a configured primary guild. Commands are blocked outside that guild through the `restrict_to_english_cafe` check in `main.py`.

This is useful for a private or community-specific deployment because it prevents commands from unintentionally operating elsewhere.

## Multi-Guild Deployment

To convert Infinity Bot into a general multi-server application, review at least the following areas:

- Remove or redesign `restrict_to_english_cafe`
- Replace assumptions around a single `BOT_GUILD_ID`
- Review guild-specific channel, role, and emoji IDs
- Review webhook configuration
- Move server-specific configuration into per-guild storage
- Review database and state isolation
- Change the application-command registration strategy
- Add per-guild initialization and teardown logic
- Verify authorization boundaries between guilds

Any state currently treated as global should be reviewed before enabling the bot across independent servers.

## Application Command Scope

Guild-scoped application commands are used intentionally during development:

```python
@app_commands.guilds(discord.Object(id=BOT_GUILD_ID))
```

They provide fast registration and updates, convenient development iteration, and isolation to the development or community server.

For a public multi-server bot, application commands can instead be registered globally. Before making that change, verify that commands do not depend on resources unique to the original guild.

## AI Integration

### Persona Responses

```text
Discord Mention / Reply
        │
        ▼
Persona Trigger
        │
        ▼
Prompt / Context Construction
        │
        ▼
OpenAI API
        │
        ▼
Generated Response
        │
        ▼
Discord Webhook
```

Persona modules can generate character-specific responses through OpenAI models and publish them through webhooks with persona-specific identities.

### Quiz Generation

```text
Source Content
     │
     ▼
Document Parsing
     │
     ▼
Text Extraction
     │
     ▼
Quiz Prompt Construction
     │
     ▼
OpenAI Async Client
     │
     ▼
Generated Questions
     │
     ▼
Discord Quiz Flow
```

Document support depends on the parser dependencies installed in the runtime. PDF, DOCX, PPTX, and XLSX parsing integrations can remain disabled or be omitted from a minimal deployment.

## Extending the Platform

With 72 existing extensions, new functionality should generally follow the established extension architecture instead of being added directly to the application bootstrap.

A minimal Cog structure looks like:

```python
from discord.ext import commands


class ExampleCog(commands.Cog):
    def __init__(self, bot: commands.Bot):
        self.bot = bot

    @commands.command()
    async def example(self, ctx: commands.Context):
        await ctx.send("Example command")


async def setup(bot: commands.Bot):
    await bot.add_cog(ExampleCog(bot))
```

Then add the extension to the application's extension-loading configuration.

For larger features, keep reusable business logic in dedicated modules instead of placing all implementation details inside the Cog:

```text
cogs/
└── economy.py
        │
        ▼
modules/
└── economy/
    ├── balances.py
    ├── rewards.py
    ├── shop.py
    ├── exchange.py
    └── models.py
```

This distinction becomes increasingly important in a codebase containing roughly 300 modules.

## Operational Considerations

### Extension Isolation

With dozens of independently loaded plugins, startup behavior should avoid allowing a failure in one optional extension to disable unrelated functionality. Useful practices include:

- Logging extension load failures
- Tracking successfully loaded plugins
- Handling optional dependencies cleanly
- Isolating external API failures
- Avoiding circular imports
- Avoiding uncontrolled global state
- Keeping extension initialization deterministic

### Error Handling

Production deployments should handle failures at appropriate boundaries, including:

- Command-level and application-command exceptions
- Discord HTTP failures and rate limits
- Missing permissions, roles, channels, or webhooks
- OpenAI and other API failures
- External service outages
- Malformed configuration
- Startup extension failures

A failure in an optional integration should ideally not terminate unrelated bot functionality.

### Rate Limits

Features that perform bulk operations should account for:

- Discord REST rate limits
- Message throughput
- Reaction operations
- Channel edits
- Role updates
- Webhook requests
- External AI request limits
- External market-data limits

Avoid unbounded request loops around Discord or third-party APIs.

### State and Persistence

Features such as XP, streaks, currency, inventories, clans, birthdays, profiles, and purchases require durable state if progress must survive process restarts.

Treat the persistence layer as authoritative application state and back it up accordingly. Where multiple tasks modify the same state concurrently, design updates to avoid race conditions and duplicate rewards.

## Security

### Secrets

Never hard-code or commit:

```text
BOT_TOKEN
OPENAI_API_KEY
API credentials
Webhook credentials
Database passwords
Private service tokens
```

Keep credentials in environment variables or a suitable secret-management system.

### Bot Token Exposure

If a Discord bot token is exposed:

1. Reset or regenerate it immediately in the Discord Developer Portal.
2. Replace it in the deployment environment.
3. Restart affected bot instances.
4. Remove the leaked credential from accessible repository history where applicable.
5. Review logs and recent bot activity for unexpected behavior.

Deleting the visible `.env` file alone is not sufficient if the secret was previously committed.

### Authorization

Sensitive commands should validate authorization server-side. Do not rely solely on hidden command names, private documentation, channel obscurity, or UI visibility.

Administrative operations should use explicit permission or role checks.

### Principle of Least Privilege

Grant the bot only the Discord permissions required by enabled modules. For example, a deployment that does not use emoji management does not need emoji-management permissions solely because the repository contains an emoji module.

## Deployment

Infinity Bot can run anywhere capable of maintaining a persistent Python process and outbound connectivity to Discord and configured external APIs.

Common deployment targets include:

- Linux VPS
- Home server
- Dedicated host
- Docker host
- Cloud VM
- Supported Python application platforms

At minimum, a production host should provide:

- A supported Python runtime
- Installed project dependencies
- Environment variables and secrets
- Stable network connectivity
- A process restart and recovery strategy
- Persistent storage where required

### Basic Linux Service Pattern

For a persistent server deployment, supervise the application with `systemd`, Docker, or another process manager. The process ultimately executes:

```bash
python main.py
```

Configure the supervisor to restart the process after unexpected failures according to the deployment policy.

## Development Workflow

A typical local workflow is:

```bash
git clone <repository-url>
cd <repository-directory>

python -m venv .venv
source .venv/bin/activate

pip install -r requirements.txt

# Configure environment variables
python main.py
```

When adding a feature:

1. Select the appropriate feature domain.
2. Determine whether the feature belongs in an existing extension.
3. Add reusable business logic to the appropriate module.
4. Add or modify the relevant Cog or plugin.
5. Add configuration where required.
6. Register or load the extension if necessary.
7. Run the bot against the development guild.
8. Verify prefix and application commands.
9. Test permissions and failure paths.
10. Review logs before deployment.

## Troubleshooting

### Prefix Commands Do Not Respond

Verify that:

- The bot is online.
- The command prefix is `!`.
- Message Content Intent is enabled if required.
- The bot can view the channel and read messages.
- The command's extension loaded successfully.
- The guild restriction is not blocking execution.

### Slash Commands Do Not Appear

Verify that:

- `BOT_GUILD_ID` is correct.
- The bot is installed in that guild.
- Application-command synchronization completed.
- The relevant extension loaded.
- The command is scoped to the expected guild.
- The bot application has the appropriate installation scope.

Guild-scoped commands should generally become available significantly faster than global commands.

### Extension Fails to Load

With 72 plugin extensions, diagnose extension-specific startup failures independently. Check for:

- Import errors
- Missing Python packages
- Missing configuration or environment variables
- Circular imports
- Invalid setup functions
- Initialization-time API failures
- Dependency changes between modules

### Role Commands Fail

Check that:

- The bot has `Manage Roles`.
- The target role is below the bot's highest role.
- The role still exists.
- Stored or configured role IDs are correct.
- Discord's managed-role restrictions do not prevent the operation.

### Persona Responses Fail

Check that:

- `OPENAI_API_KEY` is configured.
- OpenAI dependencies are installed.
- The persona extension loaded.
- The trigger is valid.
- The bot can create or use webhooks as required.
- The target channel permits webhook operations.
- API errors are not occurring upstream.

### Voice Functionality Does Not Trigger

Check that:

- Voice-state intents are enabled.
- The relevant extension is loaded.
- The bot has access to the voice channel.
- The event handler is receiving voice-state updates.
- Configured channel restrictions are correct.

### Administrative Commands Return Permission Errors

Check both the permissions of the user invoking the command and the permissions and role hierarchy of the bot itself. A user having sufficient permissions does not automatically mean the bot can perform the requested Discord operation.

## Contributing

Contributions should preserve the modular architecture of the project.

When adding a new feature:

- Place it in the most appropriate existing feature domain.
- Extend an existing plugin where appropriate.
- Create a new plugin when functionality represents a distinct subsystem.
- Keep reusable business logic outside command handlers.
- Avoid placing unrelated feature logic in `main.py`.
- Keep secrets outside source control.
- Make permission requirements explicit.
- Handle missing Discord resources and external API failures gracefully.
- Avoid unnecessary blocking operations inside async handlers.
- Validate administrative authorization before destructive actions.
- Test changes in the configured development guild before production deployment.

For substantial changes, document any new environment variables, Discord permissions, privileged intents, dependencies, external APIs, persistent data requirements, startup requirements, and extension dependencies.

## Production Checklist

Before deploying a new version, verify that:

- Dependencies install successfully.
- Required environment variables are configured.
- `BOT_GUILD_ID` points to the intended server.
- Discord privileged intents are enabled as required.
- Bot permissions match enabled functionality.
- The bot role is correctly positioned.
- All required plugin extensions load successfully.
- Extension failures are visible in logs.
- Slash commands synchronize correctly.
- Prefix commands respond correctly.
- Administrative commands enforce authorization.
- AI features handle upstream API failures.
- Persistent application data is backed up where applicable.
- No production secrets are committed to Git.
- Logs do not expose sensitive credentials.
- Startup and restart behavior has been tested.

## Technology Stack

| Technology or component | Purpose |
|---|---|
| Python 3 | Primary application language |
| `discord.py` | Discord gateway, REST API, commands, events, and application commands |
| ~300 application modules | Reusable platform and feature implementation |
| 72 plugin extensions | Independently organized Discord feature systems |
| OpenAI API | AI personas and quiz generation |
| `asyncio` and async Python | Concurrent Discord and API workflows |
| Discord Webhooks | Persona-style message delivery |
| Discord Application Commands | Slash-command interfaces |
| Prefix Commands | Traditional `!` command interfaces |
| Optional document parsers | PDF, DOCX, PPTX, and XLSX quiz sources |

## Design Goals

### Modularity

With approximately **300 modules and 72 plugin extensions**, features should remain clearly separated by responsibility.

### Extensibility

New commands, integrations, games, and progression systems should be addable without redesigning the complete application.

### Maintainability

Large feature sets should be divided into focused modules and extensions rather than oversized command files or centralized business logic.

### Operational Safety

Administrative and destructive operations should require appropriate authorization and Discord permissions.

### Community Integration

Features are designed around Discord-native interactions including messages, reactions, voice states, roles, channels, webhooks, embeds, and application commands.

### Progressive Enhancement

Optional capabilities such as AI, document parsing, and speech-to-text can be enabled without making the core Discord platform entirely dependent on those integrations.

### Scale

The architecture is intended to support a large community application containing hundreds of modules and dozens of independently organized extensions while maintaining understandable feature boundaries.

## License

This project is licensed under the **MIT License**. See [`LICENSE`](LICENSE) for the full license text.

## Author

Developed and maintained by [ak811](https://github.com/ak811).

**Related projects:** [community-votes](https://github.com/ak811/community-votes) · [temp-vc](https://github.com/ak811/temp-vc) · [threads](https://github.com/ak811/threads) · [melody-cafe](https://github.com/ak811/melody-cafe) · [owl](https://github.com/ak811/owl) · [english-cafe](https://github.com/ak811/english-cafe) · [game-of-life](https://github.com/ak811/game-of-life) · [bomb-party](https://github.com/ak811/bomb-party) · [find-the-spy](https://github.com/ak811/find-the-spy)
