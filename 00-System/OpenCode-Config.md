# OpenCode Configuration

## Working Setup (OpenRouter + Claude Sonnet 4)

```json
{
  "$schema": "https://opencode.ai/config.json",
  "model": "openrouter/anthropic/claude-sonnet-4"
}
```

## Test Result
```bash
opencode run 'Respond with exactly: OPENCODE_OPENROUTER_WORKING'
# Output: OPENCODE_OPENROUTER_WORKING
```

## Provider: OpenRouter
- Uses `OPENROUTER_API_KEY` from environment
- Default model: `openrouter/anthropic/claude-sonnet-4`
- Works out of the box with OpenRouter API key

## Local LM Studio (ornith-1.0-35b) — Not Working via OpenCode
Direct API works:
```bash
curl -X POST http://192.168.0.120:1234/v1/chat/completions \
  -H "Content-Type: application/json" \
  -d '{"model":"ornith-1.0-35b","messages":[{"role":"user","content":"test"}],"max_tokens":100,"temperature":0}'
```
But OpenCode's provider config doesn't support custom baseURL properly.

## Recommendation
Use **OpenRouter + Claude Sonnet 4** for OpenCode. It works reliably.
For local ornith-1.0-35b, use direct API calls from Python scripts (see `~/skora-content/llm_outreach_agent.py` which uses `curl` directly).