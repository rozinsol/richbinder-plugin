# RichBinder plugin for Claude

Search and read the documents you keep in RichBinder, the document binder app for Windows, from Claude. Claude can find a topic in your binders, read the matching passages, and quote them.

## Before you install

Install RichBinder from the Microsoft Store on Windows 10 or 11, and keep the app running. The plugin does not work without it. Windows only.

The plugin needs the RichBinder AI edition, or RichBinder during its 30-day trial. Starting the trial takes a second confirmation: Claude shows you the trial terms, and the trial starts only after you confirm. Approving the connection itself is done in the RichBinder app (Settings, the gear button at the top right, › AI apps), not in Claude. RichBinder must run as the same Windows user as the AI agent, and you must have chosen at least one binder when you approved that AI agent (with no binder chosen, Claude cannot read anything).

## Install as a Claude Desktop extension (.mcpb)

As an alternative to the plugin, you can install the same connection as a Claude Desktop extension. Download `richbinder-1.1.4.mcpb` from the [Releases](https://github.com/rozinsol/richbinder-plugin/releases) page, then open Claude Desktop, go to Settings > Extensions and drag the file onto that page. Double-clicking the file does not open the install window.

The extension is not signed, so Claude Desktop shows a warning that it is not verified by Anthropic. Install it only if you trust this repository.

The extension contains the same `rbctl.exe` program that ships with RichBinder 1.1.4, and it needs the same things as the plugin (see "Before you install"): RichBinder from the Microsoft Store running on Windows 10 or 11, the AI edition or the 30-day trial, and at least one binder chosen when you approve the AI agent in the RichBinder app. You can read, and only where you allow it edit or organize, the documents in the binders you approve there.

The extension file also contains the RichBinder program (governed by its Terms of Service) and third-party components under their own licenses; the notices are included in the file (`THIRD-PARTY-NOTICES.txt` and the `licenses` folder).

## What is in this repository

The plugin itself contains configuration and documentation only. It has no executable code of its own (the optional extension file in Releases also contains the RichBinder program).

- `.claude-plugin/plugin.json` describes the plugin.
- `.mcp.json` tells Claude to start one program: `rbctl.exe mcp`.
- `skills/search-binder/SKILL.md` tells Claude the order in which to use the RichBinder tools.

## What it runs

`rbctl.exe` is installed by the RichBinder app from the Microsoft Store. It is not part of this repository and is not downloaded by this plugin. `rbctl.exe mcp` speaks MCP over standard input and output and passes each call to the RichBinder app running on the same PC. The app decides what is allowed: which binders this connection may read, and whether it may change anything. The optional extension file in Releases (see "Install as a Claude Desktop extension") bundles its own copy of this program.

## What Claude can do

### Read (always read-only)

| Tool | What it does |
|---|---|
| `state` | Shows the edition, whether this connection is approved, the index status and the next step if something is blocked. |
| `guide` | Returns the RichBinder usage guide. |
| `search` | Finds matches in the binders this connection may read. The same hits are listed in the RichBinder search window. |
| `fetch` | Reads a passage of a matched document so Claude can quote it. |
| `check_decision` | Looks up records in your documents that relate to a decision text and returns them with citations. It does not judge. |
| `needs_list`, `needs_get`, `continue` | Read open-question records and the notes left for continuing earlier work. |

### Show on screen

| Tool | What it does |
|---|---|
| `open` | Opens one search hit on your screen in the RichBinder app. It changes nothing and returns no document text. |

### Change (off unless you turn it on)

These tools work only on a connection where you turned the matching permission on in the app. Otherwise the app refuses the call.

| Tool | What it does |
|---|---|
| `needs_create`, `evidence_link`, `handoff_write`, `needs_close_request` | Add an open-question record, propose evidence for it, write a handoff note, or ask you to close it. A close is only a request; you confirm it in the app. |
| `files_create` | Creates one new text document in a binder. It never overwrites an existing file. |
| `files_edit` | Replaces the text of one existing text document. You are asked in the app (allow once, always for this connection, or deny). Nothing is written unless you allow it. |
| `files_trash` | Moves documents to the Windows Recycle Bin. |
| `binders_add`, `binders_remove` | Add a folder as a binder, or remove a binder from the list. You are asked in the app every time. Removing a binder deletes no files. |

### Account

| Tool | What it does |
|---|---|
| `activate` | Starts the next account step when RichBinder blocks AI reading: signing in, starting the trial, opening the purchase page, refreshing the license, or opening the AI apps screen. Sign-up, agreeing to terms and payment are always done by you. For these steps the RichBinder app communicates with the RozinSol account server. |

## Example prompts

- Find my meeting notes about the quarterly budget review in RichBinder and summarize the decisions that were made.
- Search my RichBinder documents for the warranty period in the office printer service contract, and quote the exact sentence.
- Is RichBinder search ready on this PC?

## Setup guide

Setup for other MCP clients and troubleshooting: https://github.com/rozinsol/richbinder

## Support

Contact: support@rozinsol.com

## License

MIT. See `LICENSE`. The license covers the files in this repository only. RichBinder itself is governed by its own [Terms of Service](https://rozinsol.com/en/legal/terms/). No right is granted to the RichBinder or ROZIN Solution names or logos.

Privacy: see the [RichBinder Privacy Policy](https://richbinder.com/en/legal/privacy/) and the [RozinSol Privacy Policy](https://rozinsol.com/en/legal/privacy/).

## Trademarks

Claude is a trademark of Anthropic. This plugin is not affiliated with, endorsed by, or sponsored by Anthropic.
