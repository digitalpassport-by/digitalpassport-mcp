# Digital Passport Belarus — MCP Server & Open REST API

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![MCP Protocol](https://img.shields.io/badge/MCP-Streamable%20HTTP-green.svg)](https://digitalpassport.by/.well-known/mcp.json)
[![OpenAPI 3.1](https://img.shields.io/badge/OpenAPI-3.1.0-orange.svg)](https://digitalpassport.by/.well-known/openapi.json)

Public read-only **Model Context Protocol (MCP)** server and **OpenAPI 3.1 REST API** documentation for **[Digital Passport Belarus (digitalpassport.by)](https://digitalpassport.by)** — an open institutional directory of Belarusian legal entities backed by official state registries (EGR, GRP MNS, BelGIE) and structured company profiles.

## Features

- **Remote Streamable HTTP MCP Server:** Connect directly to `https://digitalpassport.by/api/mcp` without local installation or API keys.
- **4 Read-Only MCP Tools:**
  - `get_company_passport` — Fetch a verified company profile by 9-digit UNP or slug (`json` or `markdown`).
  - `search_belarus_companies` — Search organizations by name, UNP, city, industry rubric, specialization, or market age.
  - `explore_knowledge_graph` — Browse the two-level Belarusian business knowledge graph (broad sectors and specializations).
  - `verify_belarus_unp` — Validate the mathematical checksum of a 9-digit Belarusian UNP and identify the registration region.
- **Public REST API (OpenAPI 3.1):** `45 req/min` unauthenticated (`per_page <= 25`), or `300 req/min` with a free `dpk_` key from [digitalpassport.by/developers/api](https://digitalpassport.by/developers/api).
- **AI-Ready Discovery Endpoints:**
  - MCP Discovery: [`https://digitalpassport.by/.well-known/mcp.json`](https://digitalpassport.by/.well-known/mcp.json)
  - OpenAPI 3.1 Spec: [`https://digitalpassport.by/.well-known/openapi.json`](https://digitalpassport.by/.well-known/openapi.json)
  - AI Catalog: [`https://digitalpassport.by/.well-known/ai-catalog.json`](https://digitalpassport.by/.well-known/ai-catalog.json)
  - `llms.txt`: [`https://digitalpassport.by/llms.txt`](https://digitalpassport.by/llms.txt)

---

## Quick Start (MCP)

### Claude Desktop / Cursor / Windsurf

Add the remote MCP server to your `mcp.json` / `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "digitalpassport-belarus": {
      "type": "streamable-http",
      "url": "https://digitalpassport.by/api/mcp"
    }
  }
}
```

### Direct JSON-RPC Test (`curl`)

List available tools:

```bash
curl -s -X POST https://digitalpassport.by/api/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":1,"method":"tools/list","params":{}}'
```

Verify a 9-digit UNP checksum:

```bash
curl -s -X POST https://digitalpassport.by/api/mcp \
  -H "Content-Type: application/json" \
  -d '{"jsonrpc":"2.0","id":2,"method":"tools/call","params":{"name":"verify_belarus_unp","arguments":{"unp":"100099082"}}}'
```

---

## REST API Endpoints

See [`openapi.json`](openapi.json) or the interactive documentation at [https://digitalpassport.by/developers/api](https://digitalpassport.by/developers/api).

- `GET /api/v1/companies` — Search active Belarusian organizations (`q`, `city`, `category`, `specialization`, `per_page`).
- `GET /api/v1/companies/{identifier}` — Retrieve full structured passport JSON by UNP or company slug.
- `GET /api/v1/knowledge-graph` — Retrieve sectors, specializations, and company counts.

Example:

```bash
curl -s "https://digitalpassport.by/api/v1/companies?q=бетон&per_page=5"
```

---

## Links & Support

- Portal: [https://digitalpassport.by](https://digitalpassport.by)
- Catalog: [https://digitalpassport.by/katalog](https://digitalpassport.by/katalog)
- API Documentation: [https://digitalpassport.by/developers/api](https://digitalpassport.by/developers/api)
- Contact: `info@digitalpassport.by`
