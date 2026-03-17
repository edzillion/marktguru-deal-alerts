# Windsurf Project Rules: MarktGuru Deal Alerts

## Project 
### Stack:
- n8n automation (v2.12.2) hosted on my homelab
- Python scripts for API exploration
- Node.js snippets for n8n Function nodes

### Goals:
- scrape Marktguru API for local deals
- filter deals by keywords and price thresholds
- send alerts (method tbd)

### Key logic:
- API scraping and parsing implementation taken from here: https://github.com/thorschtn/ha-marktguru
- deal normalization
- keyword filtering
- alert deduplication

### Coding rules:
- All scripts must be idempotent
- No hardcoded secrets
- All configs in /config
- Output structured JSON

### n8n rules:
- Use Function node only for lightweight transforms
- Complex logic lives in /scripts
- Workflows exported after each change

### Logging:
- Always log:
  - API status
  - number of deals parsed
  - number of deals filtered

### Testing:
- All filter logic must have unit tests


## Code Standards

### Core Philosophy
- **No Guardrails:** Assume valid input. Do not write type-checks, null-checks, or try-catch blocks unless the logic literally cannot proceed without them.
- **No Backward Compatibility:** Use the latest syntax (Python 3.12+, Node 20+). Delete or overwrite outdated code immediately.
- **Minimalism:** No docstrings. No comments explaining "why" or "how" unless the logic is a regex nightmare.
- **Lean Code:** If a library has a built-in method, use it. Do not wrap things in unnecessary abstractions.

### Python Standards
- **Linter:** Use Black and Ruff. Commit-hook has been setup to run these on commit. 
- **Logic:** Favor list comprehensions over loops. Use `httpx` for async requests instead of `requests`.
- **Typing:** Use type hints in signatures for AI clarity, but do not validate them at runtime.

### Node.js / n8n Standards
- **Execution:** Use ESM (`import/export`).
- **n8n Nodes:** When writing code for n8n Function nodes, keep it as a single-purpose transformation. 
- **Scraping:** Use the headers and methods defined in the `ha-marktguru` repo precisely. Do not add "safety" delays unless the API blocks the request.

# Windsurf Project Rules: MarktGuru n8n Scraper

## Core Philosophy
- **Anti-Guardrail:** No type-checks, no input validation, no null-checks. Assume clean data. If it crashes, it crashes.
- **Modern Only:** No backward compatibility. Use Python 3.13+ and Node 24+. Remove all legacy or redundant code immediately.
- **Zero Documentation:** Do not write docstrings, JSDoc, or comments unless explaining a complex regex or specific MarktGuru API quirk.
- **No Chatty AI:** Do not explain changes. Do not summarize work. Code output only.

## Technical Standards
- **Python:** Use `ruff` for formatting/linting (aggressive mode). Use `pip` for dependencies. Use `httpx` for all async requests.
- **Node/JS:** Use `Biome` for linting/formatting. Use ESM only. 
- **DB:** Use `DuckDB` for local deal caching and price comparison history. 
- **n8n:** Use the "Code" node for logic. Keep n8n logic flat—no nested sub-workflows unless absolutely necessary.

## Scraping & API Rules (MarktGuru/CellarTracker)
- **Direct Access:** Bypass heavy scraping libs (BeautifulSoup/Selenium). Use the MarktGuru internal API endpoints (JSON-first).
- **Logic Mapping:** Reference `ha-marktguru` for auth headers and product ID patterns. 
- **Thresholding:** If `deal_price < (avg_price * 0.8)`, trigger n8n alert immediately. 


## Windsurf-Specific Agent Rules (Cascade)
- **Silent Overwrites:** Overwrite existing files entirely if a more concise implementation exists.
- **Fast Mode:** Use `SWE-1.5` or `Sonnet 4.6` in "No Thinking" mode to maximize velocity.

## Other

### Search & Tools
- Use `CellarTracker` API/Scraping only for the final threshold comparison.

### AI Interaction
- Do not explain changes. 
- Do not provide "Next Steps" or "Summary of changes" unless I ask.
- If I provide a URL, scrape it for the technical spec and implement it directly.
- Use a "code-first" response style.