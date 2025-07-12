# Y-Router

A Cloudflare Worker that translates between Anthropic's Claude API and OpenAI-compatible APIs, enabling you to use Claude Code with OpenRouter and other OpenAI-compatible providers.

## Quick Usage

After deploying Y-Router, add these lines to your shell configuration file (`~/.bashrc` or `~/.zshrc`):

```bash
export ANTHROPIC_BASE_URL="https://cc.yovy.app"
export ANTHROPIC_API_KEY="your-openrouter-api-key"
```

Or run Claude Code with the environment variables directly:

```bash
ANTHROPIC_BASE_URL="https://cc.yovy.app" ANTHROPIC_API_KEY="your-openrouter-api-key" claude
```

That's it! Claude Code will now use OpenRouter's models through Y-Router.

## What it does

Y-Router acts as a translation layer that:
- Accepts requests in Anthropic's API format (`/v1/messages`)
- Converts them to OpenAI's chat completions format
- Forwards to OpenRouter (or any OpenAI-compatible API)
- Translates the response back to Anthropic's format
- Supports both streaming and non-streaming responses

## Perfect for Claude Code + OpenRouter

This allows you to use [Claude Code](https://claude.ai/code) with OpenRouter's vast selection of models by:
1. Pointing Claude Code to your Y-Router deployment
2. Using your OpenRouter API key
3. Accessing any model available on OpenRouter through Claude Code's interface

## Setup

1. **Clone and deploy:**
   ```bash
   git clone <repo>
   cd y-router
   npm install -g wrangler
   wrangler deploy
   ```

2. **Set environment variables:**
   ```bash
   # Optional: defaults to https://openrouter.ai/api/v1
   wrangler secret put OPENROUTER_BASE_URL
   ```

3. **Configure Claude Code:**
   - Set API endpoint to your deployed Worker URL
   - Use your OpenRouter API key
   - Enjoy access to all OpenRouter models!

## Environment Variables

- `OPENROUTER_BASE_URL` (optional): Base URL for the target API. Defaults to `https://openrouter.ai/api/v1`

## API Usage

Send requests to `/v1/messages` using Anthropic's format:

```bash
curl -X POST https://cc.yovy.app/v1/messages \
  -H "Content-Type: application/json" \
  -H "x-api-key: your-openrouter-key" \
  -d '{
    "model": "anthropic/claude-3-sonnet",
    "messages": [{"role": "user", "content": "Hello!"}],
    "max_tokens": 100
  }'
```

## Development

```bash
npm run dev    # Start development server
npm run deploy # Deploy to Cloudflare Workers
```

## Thanks

Special thanks to these projects that inspired Y-Router:
- [claude-code-router](https://github.com/musistudio/claude-code-router)
- [claude-code-proxy](https://github.com/kiyo-e/claude-code-proxy)

## License

MIT