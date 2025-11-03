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