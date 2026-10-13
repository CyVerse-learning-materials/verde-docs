# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is the documentation repository for AI-VERDE (AI Virtual Explorer for Research, Discovery, and Education), an open source platform that facilitates access to commercial and on-premise LLMs with budget and access controls. The repository contains Zensical-based documentation for both the AI-VERDE chat interface and API.

## Architecture

- **Documentation Framework**: Zensical with the classic theme
- **Content Structure**: 
  - `docs/` - Main documentation content
  - `docs/api/` - API documentation and integration guides
  - `docs/instructors/` - Instructor-specific documentation
  - `docs/assets/` - Images and static assets
- **Configuration**: `zensical.toml` - Site configuration and navigation
- **Styling**: `docs/stylesheets/extra.css` - Custom CSS defining the `aiverde` light color scheme used in `zensical.toml`

## Development Commands

### Local Development
```bash
# Install dependencies
pip install -r requirements.txt

# Serve documentation locally with live reload
zensical serve

# Build static site
zensical build --clean --strict
```

The GitHub Actions workflow in `.github/workflows/ghpages.yml` deploys the generated `site/` directory to the `gh-pages` branch on pushes to `main`.

### Content Management
- Documentation is written in Markdown
- Images should be placed in `docs/assets/`
- New pages must be added to the `nav` section in `zensical.toml`

## Key Documentation Sections

- **AI-VERDE Chat**: User guides for the chat interface
- **AI-VERDE API**: API key and model list guides, plus integration guides for AWS Bedrock (Claude Code, Claude Code for VS Code), Python libraries (LangChain, LlamaIndex, Anthropic Python SDK), CLI coding assistants (Claude Code Router, Aider, Claude Code, Codex, OpenCode), IDEs (VSCode), and desktop clients (ChatboxAI)
- **For Instructors**: Course creation and management guides

## Content Guidelines

- Screenshots and images are heavily used for user guidance
- API key examples are provided for multiple platforms and environments
- Documentation targets university/educational use cases
- Content assumes institutional authentication (currently University of Arizona) via CILogon, where UArizona users pick "The University of Arizona" as their identity provider
- Support contact is `ai-verde-support@cyverse.org`; course setup is requested by email (no form), and rosters are added by instructors in the Members tab or emailed to support
- Budgets are set by CyVerse staff only (there is no budget UI for instructors)

## API Conventions

Keep integration guides consistent with these rules (summarized for readers in `docs/api/index.md`):

- **Base URLs**: OpenAI-compatible clients use `https://llm-api.cyverse.ai/v1`; Anthropic-style clients (Claude Code, Anthropic SDK) use `https://llm-api.cyverse.ai`; AWS Bedrock uses `https://llm-api.cyverse.ai/bedrock`, and the Bedrock-style API is reserved for Claude Code only (the Anthropic SDK uses the Anthropic-style API). LiteLLM `litellm_proxy` examples (LangChain, LlamaIndex) use the URL without `/v1`.
- **Claude Code key variable**: non-Bedrock pages use `ANTHROPIC_API_KEY`; Bedrock pages must use `ANTHROPIC_AUTH_TOKEN`, because Claude Code only sends that variable on the Bedrock route.
- **Claude Code persistence**: document the `env` block in `~/.claude/settings.json` first and shell-profile exports second. Claude Code does not write exported variables into `settings.json`. The Claude Code for VS Code extension is the exception: configure it only through `claudeCode.environmentVariables`, since `~/.claude/settings.json` does not reach the extension's login check.
- **Model names**: AI-VERDE model names are prefixed with a course/team identifier joined by a dash or slash (e.g. `my-team-claude-sonnet-4-6` or `my-team/claude-sonnet-4-6`). Point readers to `api/api-key-models.md`, not to providers' public model lists.