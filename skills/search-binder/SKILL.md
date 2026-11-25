---
name: search-binder
description: Search the RichBinder documents on this PC and quote them. Use when the user asks what their RichBinder documents say about a topic.
---

# Search RichBinder documents

Use the RichBinder tools in this order.

1. If the search may not work, call `state` first and tell the user what it says.
2. Call `search` with the user's topic. Use the best hits.
3. Call `fetch` on the hits you need to read or quote. Quote from `fetch` only.

If `search` finds nothing, say so. Do not guess the contents of a document.
