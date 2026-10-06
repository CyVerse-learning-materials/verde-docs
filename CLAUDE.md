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
- **Styling**: `docs/stylesheets/extra.css` - Custom CSS

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
- **AI-VERDE API**: API documentation and integration examples for LangChain, LlamaIndex, and VSCode
- **For Instructors**: Course creation and management guides

## Content Guidelines

- Screenshots and images are heavily used for user guidance
- API token examples are provided for multiple platforms and environments
- Documentation targets university/educational use cases
- Content assumes institutional authentication (currently University of Arizona)