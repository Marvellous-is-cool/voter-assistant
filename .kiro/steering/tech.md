# Tech stack and conventions

## Stack
- Python 3.12, FastAPI, Pydantic v2
- httpx for outbound HTTP (channel APIs, LLM providers)
- SQLite via SQLAlchemy 2.x for the MVP (swap to Postgres later without code changes)
- APScheduler for reminders
- pytest + pytest-asyncio for tests; ruff for linting and formatting
- Docker for deployment

## Architecture rules
- **One brain, many front doors.** All channels (Telegram, WhatsApp, web) are thin
  adapters that convert platform messages into a common `IncomingMessage` and render a
  common `BotReply`. No business logic inside channel adapters.
- **Conversation engine is channel-agnostic.** It takes an `IncomingMessage` plus the
  user's session and returns a `BotReply`. Pure and easy to unit test.
- **Country packs are data, not code.** Each pack lives in `packs/<country_code>/` as
  YAML: `pack.yaml` (languages, election body, official links), `messages/<lang>.yaml`
  (all bot strings), `faq/<lang>.yaml` (official Q&A), `sample_data.yaml` (demo voters).
  Adding a country must not require Python changes.
- **LLM behind an interface.** A `LLMProvider` protocol with at least one implementation.
  The LLM is used for intent detection and for answering free-text questions *only*
  from retrieved pack content. Every LLM call has a deterministic fallback
  (keyword/menu matching) so the bot still works if the LLM is down.
- **Data access behind an interface.** A `VoterRecordSource` protocol. The MVP uses
  `SampleDataSource`, reading `sample_data.yaml`. Real integrations can be added later.

## Conventions
- Type hints everywhere; Pydantic models for all data crossing boundaries
- Config via environment variables (pydantic-settings); never commit secrets; keep a
  `.env.example`
- Every user-facing string comes from the pack's `messages/<lang>.yaml`, never hard-coded
- Tests for every intent in every language of the Nigeria pack
- Log events without personal data
