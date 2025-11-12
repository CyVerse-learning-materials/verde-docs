# Claude Code (using Anthropic Models)

This guide explains how to connect Claude Code with your AI-VERDE API Key to access Anthropic models through CyVerse. 

Follow the steps below after installing Claude Code to configure your connection. For more details on Claude Code features and usage, visit the [Anthropic documentation](https://docs.anthropic.com/en/docs/intro).

!!! Note

    Use this setup if your workspace supports **Anthropic LLMs** (like Claude 3 Sonnet or Opus). If your workspace uses **non-Anthropic models** (such as OpenAI, Gemini, or other providers), follow the [Claude Code Router setup](claude-code-router.md).  

## Prerequisites

1. Your VERDE course or team must be configured to use Anthropic models (see instructor or team lead) 
2. Obtain your VERDE API Key follow the [AI-VERDE API Token Guide](api-token.md)
3. Install Claude Code. Instructions can be found here, [Anthropic’s website](https://www.anthropic.com/claude-code/).
4. A terminal (bash) open on a system where Claude Code is installed.

## 1. Setting up the necessary environment variables

This step should only be needed the first time you use Claude Code.

In a terminal, set the following environment variables and replace `ANTHROPIC_API_KEY` to your VERDE API Key.
```
export ANTHROPIC_BASE_URL="https://llm-api.cyverse.ai"
export ANTHROPIC_API_KEY="insert-VERDE-API-Key-here"
export ANTHROPIC_MODEL="anthropic/claude-sonnet-4"
```

Note, the `ANTHROPIC_MODEL` can be set to any available Anthropic model. Information about available models can be found here, [Anthropic documentation](https://docs.anthropic.com/en/docs/about-claude/models/overview).

## 2. Launch Claude Code

After setting your environment variables, start Claude Code by entering:
```
claude
```
After initially launching Claude Code, claude will write the variables into a `~/.claude/settings.json` file. You do not need to repeat step #1 again for future sessions.

## If you need to change your `ANTHROPIC_API_KEY`

If for some reason you need to change your VERDE API Key, you can use the slash command `/logout` in claude or delete your `~/.claude/settings.json`; then, repeat steps 1-2.