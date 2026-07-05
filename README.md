# claude-science-byok

A reusable **Hermes Agent skill** that installs and runs Anthropic's [Claude Science](https://claude.com/product/claude-science) **without a Claude account**, powered by **any** OpenAI- or Anthropic-compatible API.

Solves two pain points for users in mainland China (and anyone without a Claude Pro/Max subscription):
1. **Install blocked** — `claude.ai` is geo-blocked. This skill downloads the binary from the unblocked `downloads.claude.ai` CDN.
2. **Login required** — fakes a local OAuth token + patches the binary so no Claude subscription is needed; routes all traffic to your own API via [claude-science-api-bridge](https://github.com/Jyx0208/claude-science-api-bridge).

## Supported backends (not limited to any one provider)

| Provider | Mode | Example model |
|---|---|---|
| Volcengine Ark (火山引擎) | anthropic / openai | glm-5.2 |
| DeepSeek | anthropic / openai | deepseek-chat |
| Zhipu / z.ai (智谱) | openai | glm-4.6 |
| SiliconFlow (Kimi/Qwen) | openai | Pro/moonshotai/Kimi-K2.6 |
| OpenAI | openai | gpt-4o |
| Local Ollama / vLLM | openai | any |
| OneAPI / NewAPI relay | openai | any |

## Install as a Hermes skill

```bash
# Clone into your Hermes skills directory
git clone https://github.com/8lampard8/claude-science-byok.git \
  ~/.hermes/skills/software-development/claude-science-byok
```

Then in any Hermes session, the skill auto-loads when you ask to install/use Claude Science.

## Install manually (without Hermes)

Just follow `SKILL.md` — it's a standalone step-by-step guide. The `scripts/` and `references/` are usable on their own.

## Contents

```
SKILL.md                              # full guide (frontmatter + steps + pitfalls)
scripts/install-claude-science.sh     # download + SHA256-verify + install binary
scripts/cs-start.sh                   # one-click launcher
references/providers.md               # ready-made configs for 8 providers
patches/volcengine-v3-url-fix.patch   # fix /v3 URL normalization for Volcengine
```

## Safety

- No API keys are stored in this repo — all configs use `***` placeholders.
- `.gitignore` excludes `config.json`, `.env`, `*.key`, `*.enc`.
- The binary patch only rewrites OAuth validation URLs to point at the local bridge.

## License

MIT. Upstream proxy project: [Jyx0208/claude-science-api-bridge](https://github.com/Jyx0208/claude-science-api-bridge) (MIT).
