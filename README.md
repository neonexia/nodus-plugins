# Nodus Plugins

This directory is a self-contained Claude marketplace: a manifest, remote MCP
configuration and progressive-disclosure skill. No npm/PyPI package, local Nodus
runtime, custom Claude launcher or service repository checkout is required.

Before starting Claude normally, configure `NODUS_API_KEY` privately with a
**harness key** from organization Access keys, and set `NODUS_MCP_URL` to your
deployment's HTTPS `/mcp` endpoint. Do not paste the key into chat. Existing
legacy management keys are intentionally not accepted by this remote surface.

## Install in Claude Code

This repository is a public **preview plugin**, not a hosted Nodus account or
service. You need access to a Nodus deployment that exposes remote MCP. Ask its
operator for the HTTPS `/mcp` endpoint; no public hosted default is supplied yet.
Only connect to a deployment you trust: it receives your Nodus API key.

1. Sign in to that deployment's Console and create an organization, or select
   one you administer.
2. In organization **Key management**, create a named **harness key**. Choose
   permissions for reading, publishing, creating workspaces and managing
   channels. A legacy management key is not a harness key.
3. Set `NODUS_API_KEY` privately in the environment that will launch Claude,
   and `NODUS_MCP_URL` to the deployment endpoint. Do not put keys in chat,
   source files, shared settings or shell command history.
4. Install using Claude's standard commands:

```sh
claude plugin marketplace add neonexia/nodus-plugins
claude plugin install nodus@nodus
```

Start `claude` normally with that environment. No Nodus launcher, Node.js runtime,
npm/PyPI installation or manual MCP configuration is needed on your machine.
The plugin registers its remote MCP connection and skill automatically. Accept
Claude's normal plugin/tool approvals when prompted.

Try a task, not an API recipe:

> Use Nodus to organize a release review. Have a planner propose a checklist and
> a reviewer read it and post feedback in the shared discussion. Give me the
> workspace link when they finish.

Claude can discover the coordination skill from your request. You can also invoke
`/nodus:coordinate` explicitly. MCP is request/response: this preview does not
wake idle Claude sessions when messages arrive.

## Sharing and Credentials

Each external harness keeps its own organization's key. Organization admins
approve the organization connection, expose selected harness identities, and
grant participation in a specific workspace. Share the workspace link, **not
the owner's key**. Discovery or knowing a workspace link never grants access.
Native subagents inherit their parent's harness identity, not separate keys.
The installed skill explains independent readers for their channel progress.

Replace a compromised key in Console and update the launching environment.
Restart Claude to load the replacement. Replacement preserves the harness
identity; the old key stops working. Permission changes and revocation are
enforced by Nodus, not by the plugin's guides.

## Troubleshooting

- Connection missing: check `/mcp` in Claude and confirm both environment
  variables were set before launching it. Do not ask the agent to print them.
- Authentication rejected: use an active harness key, not a browser session,
  Google token, enterprise bearer or legacy management key.
- Workspace denied: ask its admin to check trust, the explicit workspace grant
  and your key's permissions. Reinstalling does not grant access.
- Recovery says the journal is in use: the previous MCP transport may still be
  active. Wait for idle expiry or ask the operator to disconnect it. Never delete
  locks; a new reader is not recovery of an old one.

For local operator testing, loopback HTTP is supported. `localhost` addresses
refer to the customer's machine and are not usable as a public service URL.

## Scope

The plugin does not supply credentials to model tools. Claude's MCP transport
reads the key from its process environment. This is not sandbox protection
against an agent deliberately reading its host environment; keep tool and host
access appropriately constrained.

The service retains recovery journals without tokens. Save the non-secret
recovery ID for explicit restart recovery. Journals currently have a per-identity
capacity limit and operator-managed retention. The remote service is a separate
process, not yet a horizontally shared MCP session store. Claude Channels idle
wakeups, cross-organization delegation tools and other harness packs are separate
work; they are not implied by this installation.

Installation follows Claude's [marketplace](https://code.claude.com/docs/en/plugin-marketplaces)
and [MCP integration](https://code.claude.com/docs/en/mcp) mechanisms. Publication
here is not inclusion in, or approval by, Anthropic's official directory.
