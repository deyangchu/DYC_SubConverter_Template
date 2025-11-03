# AI Agent Instructions for DYC_SubConverter_Template

Purpose
- Short, actionable guidance so an AI coding agent can safely and productively edit rule templates and configuration used by SubConverter.

Big picture (what this repo is)
- This is a template repository of routing rule lists and a central `general.ini` that assembles them into rulesets consumed by SubConverter/Clash/Surge-like tools.
- Rule files live at repository root (e.g. `dyc_directList.list`, `dyc_proxyList.list`, `dyc_usaList`, `ChatGPT.list`, `TikTok.list`).
- `general.ini` lists ruleset sources (remote and local), defines proxy groups (`custom_proxy_group=` entries), and sets generator flags.

Key patterns you must follow (concrete examples)
- Rule list lines use these exact formats (examples found in this repo):
  - DOMAIN-SUFFIX,example.com
  - DOMAIN-KEYWORD,keyword
  - IP-CIDR,192.168.1.0/24
- Add a ruleset in `general.ini` using the existing pattern:
  ruleset=🎯 全球直连,https://raw.githubusercontent.com/deyangchu/DYC_SubConverter_Template/main/dyc_directList.list
  (You can also reference remote sources like ACL4SSR or Blackmatrix7—see many examples already present in `general.ini`.)
- Proxy group configuration follows the `custom_proxy_group=` syntax. Common types used here:
  - `select` (manual selection), `url-test` (probe-based selection), `fallback`, `load-balance`.
  - Example (from `general.ini`):
    custom_proxy_group=♻️ 自动选择`url-test`.*`http://www.gstatic.com/generate_204`300,,50

Important repo flags and their meaning (discoverable in `general.ini`)
- `enable_rule_generator=true` — the repo expects an automated generator/processor to produce final rule outputs.
- `overwrite_original_rules=true` — generator intends to replace source lists when enabled.

Integration points and external dependencies
- `general.ini` contains many remote ruleset URLs (ACL4SSR, DivineEngine, blackmatrix7). When editing, prefer to keep existing upstream references intact unless intentionally replacing them.
- The repo is a template for SubConverter workflows — changes to lists or `general.ini` are typically meant to be published to a raw URL (GitHub) and consumed by client devices.

Developer workflow (concrete, repeatable)
1. Edit or add rules in the appropriate file under the repo root (choose list by purpose: `dyc_proxyList.list` for proxy rules, `dyc_directList.list` for direct, `dyc_usaList` for US-specific).
2. If the rule should be included in the export, ensure `general.ini` contains a `ruleset=` line that points to the file (remote raw GitHub URL or local path consistent with examples).
3. Preserve emoji-prefixed group names and ordering — these encode human-readable groups used by clients and may affect priority.
4. Commit and push. The generator or client will pull the raw GitHub URL listed in `general.ini`.

Edge cases and gotchas (observed in repo)
- The `ruleset=` line format supports optional type prefixes (`surge:`, `quanx:`, `clash-domain:`) — do not add a type unless you know the consumer requires it.
- Some rulesets use special tokens like `[]GEOIP,CN` or `[]FINAL`. Keep these as-is when present because they express semantic fall-through rules.
- `custom_proxy_group` lines contain embedded backtick-delimited parameters — preserve punctuation and pattern syntax exactly.

Files to reference when editing
- `general.ini` — authoritative assembly file (read before changing lists)
- `dyc_directList.list`, `dyc_proxyList.list`, `dyc_usaList`, `ChatGPT.list`, `TikTok.list` — rule sources and canonical examples
- `README.md` — general repository purpose and any high-level notes

If you need to change behavior not discoverable from repo files
- Ask: is this an intentional semantic change (new group semantics, different upstream source)? If yes, request maintainers' confirmation before altering `ruleset=` lines or `custom_proxy_group` semantics.

What I changed and why
- This file condenses the original long-form guidance into a concise, actionable reference that points to exact files and examples in the repo.

Questions for the maintainer
- Should new lists be placed in a `rules/` folder instead of repo root? (current repo uses root files.)
- Are there any CI or generator scripts (not in repo) that run against this template that the agent should invoke or be aware of?

Please review these instructions and tell me any missing local workflows (CI, generator commands, or external services) you want me to include.
# AI Agent Instructions for DYC_SubConverter_Template

## Project Overview
This repository contains customized rule templates for SubConverter, a tool used to convert between different proxy subscription formats. The project primarily focuses on managing proxy routing rules for different services and regions.

## Key Components

### Rule Lists
- `dyc_directList.list`: Direct connection rules
- `dyc_proxyList.list`: Proxy routing rules
- `dyc_usaList`: US-specific routing rules
- `ChatGPT.list`: Rules for AI services (OpenAI, Bing, etc.)
- `TikTok.list`: TikTok-specific routing rules

### Configuration Files
- `general.ini`: Main configuration file that:
  - Defines DNS settings
  - References external rule sources
  - Sets up rule groups and their priorities
  - Integrates with ACL4SSR and other common rule sources
- `generalWithAdblock.ini`: Extended configuration including ad-blocking rules

## File Format Conventions

### Rule List Format
Rules follow these formats:
```
DOMAIN-SUFFIX,example.com
DOMAIN-KEYWORD,keyword
IP-CIDR,192.168.1.0/24
```

### INI Configuration Structure
- Uses semicolon (;) for comments
- Sections are defined with [section_name]
- Ruleset format: `ruleset=GroupName,URL/Path,UpdateInterval`

## Working with the Codebase

### Adding New Rules
1. Choose the appropriate list file based on the rule type:
   - US-specific rules → `dyc_usaList`
   - Direct connection rules → `dyc_directList.list`
   - Proxy rules → `dyc_proxyList.list`
2. Follow the established format for the rule type
3. Update the relevant INI file if needed to include the new ruleset

### Best Practices
- Keep rules organized by category and purpose
- Use DOMAIN-SUFFIX for entire domains, DOMAIN-KEYWORD for flexible matching
- Include comments for non-obvious rules
- Reference official sources (ACL4SSR, DivineEngine) for rule patterns

## External Dependencies
- ACL4SSR rules
- Blackmatrix7 rules
- DivineEngine rules