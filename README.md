<p align="center">
  <img src="assets/voicemoat-icon-512.png" alt="VoiceMoat" width="96" height="96">
</p>

# VoiceMoat MCP server

The personal brand OS for LinkedIn and Twitter: draft in your voice, check drafts
for Style and Stance, read your analytics, and schedule or publish with a preview
first, from more than 20 AI assistants, including Claude, ChatGPT, Cursor,
Gemini, Grok, Manus and Perplexity Computer.

**This repository holds documentation and connection settings only.** The
server is a hosted service run by VoiceMoat at the address below. Its source
code is not public, and there is nothing here to run. `plugin.json` and
`mcp.json` follow the [Agent Plugins](https://open-plugins.com) standard, and
`.claude-plugin/` with `.mcp.json` make the same settings a Claude Code plugin.
All of them only point a client at that address.

```
https://app.voicemoat.com/api/mcp
```

| | |
|---|---|
| Transport | Streamable HTTP (remote, hosted) |
| Authentication | Sign-in (OAuth) for most assistants. A personal key for assistants that can only send a fixed header |
| Requires | A VoiceMoat account on **Pro** or **Enterprise**, or the **$5 Pro trial** |
| Website | https://voicemoat.com/mcp |
| Full setup guide | https://docs.voicemoat.com/connect-voicemoat-to-an-assistant |
| Guide for each assistant | https://docs.voicemoat.com/assistants |
| Official MCP Registry | `com.voicemoat/voicemoat` |

Connecting works on any plan. If your plan does not include it, each tool
refuses with an explanation, and it starts working when you move to Pro,
Enterprise or the $5 Pro trial, without reconnecting.

## What it does

- Check a draft against your voice profile, built from your own published posts
  and kept separately for each platform. Style shows how many of your measurable
  habits it matches. Stance shows whether any line says something you would not.
  The two are never blended into one number.
- Improve a draft you already have.
- Get post ideas and opening lines.
- Read your voice profile, your impressions and reactions, and your top posts
  for the last 30 days.
- Publish a post now or schedule it, on Twitter or LinkedIn.

You do not call tools by name. You ask for what you want and the assistant picks.

## Connect it

**Claude**

1. Open **Settings**, then **Connectors**.
2. Choose **Add custom connector**.
3. Name it VoiceMoat and paste the address above.
4. Select **Connect** and sign in to VoiceMoat.

**ChatGPT**

Until VoiceMoat is listed in ChatGPT's plugin directory, add it with developer
mode. Whether you can turn developer mode on depends on your ChatGPT account and
workspace.

1. Open **Settings**, then **Security and login**, and turn on **Developer mode**.
2. Open **Plugins** and select the plus button.
3. Name it VoiceMoat, paste the address under **Connection**, and create it.
4. Sign in to VoiceMoat when asked.

**Grok**

1. Open grok.com/connectors.
2. Choose **New Connector**, then **Custom**.
3. Paste the address.
4. Sign in to VoiceMoat when asked.

**Claude Code**

As a plugin:

```
/plugin marketplace add voicemoat/voicemoat-mcp
/plugin install voicemoat@voicemoat-mcp
```

Or add the server on its own:

```
claude mcp add -t http voicemoat https://app.voicemoat.com/api/mcp
```

Either way, type `/mcp` to sign in.

**Cursor**

Add the server to `~/.cursor/mcp.json`, or to `.cursor/mcp.json` in a project:

```json
{
  "mcpServers": {
    "voicemoat": {
      "url": "https://app.voicemoat.com/api/mcp"
    }
  }
}
```

Then sign in to VoiceMoat when Cursor asks.

**Gemini CLI**

Install it as an extension:

```
gemini extensions install https://github.com/voicemoat/voicemoat-mcp
```

Then run `/mcp auth voicemoat` and sign in to VoiceMoat.

**Terminal (VoiceMoat CLI)**

No assistant needed: the same tools from your terminal or scripts.

```
npx voicemoat login
npx voicemoat ideas "remote work" --platform linkedin
```

Posting still previews first; `voicemoat confirm <id>` posts. Source and the
agent skill: https://github.com/voicemoat/voicemoat-cli

**Grok Build**

```
grok mcp add --transport http voicemoat https://app.voicemoat.com/api/mcp
```

Grok Build opens the browser the first time; sign in to VoiceMoat.

**Cline**

1. In the Cline panel, select the wrench icon, then the **MCP** tab.
2. Choose **Add Remote Server**, name it VoiceMoat and paste the address above.
3. Sign in to VoiceMoat in the browser window Cline opens. Once connected,
   VoiceMoat shows a green dot and its 15 tools.

**Assistants that use a personal key**

Manus, Cue, nanoclaw, DeepSeek Harness and Perplexity Computer can only send a
fixed header, so they connect with a personal key.

1. In VoiceMoat, open **Settings**, then **Assistants**, then **Personal keys**.
2. Press **Create key** and pick the assistant. Tick **publish** if it should be
   able to post straight away.
3. Copy the key, which shows once, and send it as the header
   `Authorization: Bearer` followed by the key.

The key can be revoked at any time. VoiceMoat keeps only a fingerprint of it.
There is a setup guide for each assistant at https://docs.voicemoat.com/assistants

**Other clients**

Any client that supports remote MCP servers over Streamable HTTP, with OAuth or
a fixed header, can connect with the same address. Nothing is shared until you
connect, and the connection only ever reaches your own account.

## Tools (15)

| Tool | What it does | Read only | Posts |
|---|---|---|---|
| `get_me` | Which VoiceMoat account is connected, and its plan | Yes | No |
| `list_profiles` | Your connected Twitter and LinkedIn profiles | Yes | No |
| `get_voice_profile` | Your trained voice profile for a platform | Yes | No |
| `get_voice_insights` | Your Voice Lab analysis, when you have run it | Yes | No |
| `get_analytics` | Totals and the top post for a window (up to 30 days) | Yes | No |
| `list_posts` | Your best posts in a window | Yes | No |
| `get_post` | One post in full, with its numbers | Yes | No |
| `list_creators` | Creators you study in VoiceMoat | Yes | No |
| `search_inspiration` | Public LinkedIn posts from tracked creators, by topic (not offered in ChatGPT) | Yes | No |
| `score_voice_match` | Check text for Style and Stance against your voice profile | No (uses credits) | No |
| `get_post_ideas` | Post ideas on a topic | No (uses credits) | No |
| `improve_post` | Improve a draft | No (uses credits) | No |
| `suggest_hooks` | Three opening lines for a topic | No (uses credits) | No |
| `publish_post` | Publish now, after a preview and a confirmed second call | No | Yes |
| `schedule_post` | Schedule for later, same preview and confirmation | No | Yes |

Reading costs no credits. Checks, ideas, hooks and improving spend credits from
the same pool as the VoiceMoat dashboard, at the same prices.

## Posting always asks twice

Neither posting tool acts the first time it is called.

1. The assistant calls it. Nothing is posted. It gets back the exact text, the
   account the post would go to, and a one-time confirmation code.
2. Only a second call carrying that code posts anything.

The code is tied to the exact text, the exact account and you. If anything
changes between the two calls, it is refused and a fresh preview is returned. It
works once, so the same approval cannot post twice.

The second call is not you approving the post. An assistant can make it on its
own, so keep your assistant's tool approval on if you want to see every post
before it goes out.

## Network and credentials

- **One endpoint:** `https://app.voicemoat.com/api/mcp` over HTTPS (Streamable HTTP). Nothing runs on your machine: this repo has no scripts, hooks, binaries or dependencies, only settings files and docs.
- **Credentials:** OAuth sign-in with your VoiceMoat account, or a personal key you create in Settings. No keys are stored in this repo or in the plugin; your assistant keeps the sign-in token or key. Your Twitter and LinkedIn logins stay with VoiceMoat and are never shared with the assistant.
- **What it touches:** your own VoiceMoat account only: your voice profile, posts and analytics. Posting needs a preview and a second call with a one-time code.

## Limitations

- Works only with your own account and the profiles you connected.
- Your assistant creates new drafts; VoiceMoat checks, improves, schedules and
  publishes them.
- Style and Stance describe how close a draft is to your own posts. They do not
  predict performance.
- It cannot attach images, delete posts, reply to other people's posts or send
  messages.
- LinkedIn numbers are as fresh as your last LinkedIn sync.

## No account?

The free VoiceMoat skills work in Claude, ChatGPT and Codex without one:
https://github.com/prateeks367/voicemoat-skills

Install all 26 into Claude Code, Codex, Cursor, OpenClaw, Hermes and other
agents with [skills.sh](https://skills.sh/prateeks367/voicemoat-skills):

```
npx skills add prateeks367/voicemoat-skills
```

Add `--skill write-in-my-voice` for one skill, or `-g` to install them for
every project.

## Also listed on

- [Claude directory](https://claude.ai/directory/voicemoat)
- [Glama](https://glama.ai/mcp/connectors/com.voicemoat/voicemoat)
- [MCP Market](https://mcpmarket.com/server/voicemoat)

[![AllMCPs Verified](https://allmcps.com/api/badge/voicemoat)](https://allmcps.com/mcp/voicemoat?verify=0629bb89-a7bb-45e3-b534-07d176d7157c)

## Links

- Privacy: https://voicemoat.com/privacy
- Terms: https://voicemoat.com/terms
- Support: https://voicemoat.com/contact or founder@voicemoat.com

`server.json` in this repository is the entry published to the Official MCP
Registry.

## License

The documentation and connection settings in this repository are under the
MIT license; see [LICENSE](LICENSE). The license does not cover the VoiceMoat
service or its server code, which are not public.
