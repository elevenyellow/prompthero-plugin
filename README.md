# PromptHero

Create AI images and videos from a conversation. This plugin connects your assistant to your PromptHero account through a remote MCP server.

**Pre-launch:** the plugin package is prepared for marketplace submission. The public MCP service and Grok Bot listing are not live yet. Publishing this repository does not make the connector available in Grok Bot.

## Connect

Once the service and marketplace listing are live:

1. In Grok Bot, open **Settings → Plugins → Marketplace** and add **PromptHero**.
2. Connect your PromptHero account in the browser and approve access.
3. Attach PromptHero to your conversation and describe what you want to create.

Cursor users can install the published plugin from the marketplace, or add this remote server in their MCP settings once the service is live:

```json
{
  "mcpServers": {
    "prompthero": {
      "url": "https://mcp.prompthero.com/mcp"
    }
  }
}
```

Authentication uses browser-based OAuth. You do not paste API keys, provider credentials, or a PromptHero password into the plugin. You need a PromptHero account and sufficient credits for generation. Model availability, credit costs, and private-generation eligibility depend on your account and the selected model.

## What you can do

| Tool | Capability |
| --- | --- |
| `list_models` | Discover available image/video models, input requirements, and estimated credit costs. |
| `get_account` | Check your connected account's credit balance. |
| `generate` | Submit an image or video generation with an explicit public/private choice. |
| `get_generation` | Check your generation's status and retrieve its output URL when ready. |
| `get_generation_request` | Recover a previous submission using its request ID. |

Try asking:

- “Help me create a premium skincare product ad on a soft pink background. Show me suitable models and the estimated credits, then confirm visibility before generating.”
- “Create a cinematic motorcycle scene in a rain-soaked neon city. Find a suitable image model and explain the cost before starting.”
- “Plan a short vertical video about a lone explorer on another planet. Check the available video models and supported duration before we generate it.”

The assistant should discover models first, follow the returned input requirements, and use one request UUID per intended generation. Retrying an identical submission must retain that UUID. If a request is pending or uncertain, look it up before starting anything new. Poll a generation at least five seconds apart.

Generation uses PromptHero's normal credits, subscription rules, and moderation. The plugin cannot purchase credits, administer accounts, upload local files, or retrieve another user's private generations. Output URLs are returned to the assistant; how media is displayed depends on the client.

## Package

This is a Cursor-format MCP plugin for the marketplace used by Grok Bot. It contains only the manifest, remote server configuration, documentation, and PromptHero icon. It does not include the PromptHero application or backend source.

- [PromptHero](https://prompthero.com)
- [Connection guide](https://prompthero.com/mcp)
- [Grok Bot plugins](https://docs.x.ai/grok-bot/computer-and-apps)
- [Cursor plugin format](https://cursor.com/docs/reference/plugins)

Native Grok Bot installation and public OAuth remain release checks. The MCP implementation has been tested locally with the official MCP SDK, including a real image generation; this does not establish marketplace approval or native-client interoperability.
