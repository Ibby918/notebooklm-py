---
name: notebooklm-py
description: Use when the user wants to generate content from Google NotebookLM — audio podcasts, quizzes, flashcards, mind maps, slide decks, infographics, or data tables. Triggers on "generate a quiz", "make flashcards", "create a podcast", "download quiz as JSON", "generate a mind map", "slide deck from my research", or any NotebookLM content generation request.
---

# NotebookLM Python — Content Generation from NotebookLM

Full Python API and CLI. Generates and downloads audio, video, quizzes, flashcards, mind
maps, slide decks and data tables — including features the web UI doesn't expose.

**Requires:**
```bash
pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login    # Opens Chrome to authenticate
```

## When to Use

- Generating quizzes, flashcards, podcasts, mind maps, or slide decks from a notebook
- Downloading artifacts locally (JSON, MP3, PDF, PPTX, CSV)
- Automating NotebookLM content workflows from Python scripts

**Prefer this over `notebooklm-mcp-cli` when:** You want content generation and downloads. Use `notebooklm-mcp-cli` for notebook/source management.

**Skip when:** The user just wants to query a notebook — use `nlm notebook query` instead.

## CLI Quick Reference

```bash
# Setup
notebooklm create "My Research"
notebooklm source add "https://example.com"
notebooklm source add "./paper.pdf"
notebooklm ask "What are the main conclusions?"

# Generate (add --wait to block until done)
notebooklm generate audio --wait
notebooklm generate quiz --difficulty hard
notebooklm generate flashcards --quantity more
notebooklm generate slide-deck --wait
notebooklm generate mind-map
notebooklm generate infographic --orientation portrait
notebooklm generate data-table "compare key metrics"

# Download
notebooklm download audio ./podcast.mp3
notebooklm download quiz --format json ./quiz.json
notebooklm download quiz --format markdown ./quiz.md
notebooklm download flashcards --format json ./cards.json
notebooklm download slide-deck ./slides.pdf        # or .pptx
notebooklm download mind-map ./mindmap.json
notebooklm download data-table ./data.csv

# Slash command
/notebooklm
```

## Content Types & Formats

| Type | Output Formats | Web UI? |
|---|---|---|
| Audio Overview | MP3/MP4 (deep-dive, brief, critique, debate) | ✅ |
| Quiz | JSON, Markdown, HTML | ❌ download only here |
| Flashcards | JSON, Markdown, HTML | ❌ download only here |
| Slide Deck | **PPTX** (editable), PDF | ❌ PPTX only here |
| Mind Map | JSON (hierarchical) | ❌ export only here |
| Data Table | CSV | ❌ export only here |
| Infographic | PNG (portrait/landscape) | ✅ |

## Trading & Study Workflows

```bash
# Study materials from strategy docs
notebooklm create "Trading Strategy Notes"
notebooklm source add "./parity-engine-docs.md"
notebooklm generate quiz --difficulty medium --wait
notebooklm download quiz --format json ./strategy-quiz.json

# Research podcast
notebooklm generate audio --wait
notebooklm download audio ./morning-brief.mp3
```

## Common Mistakes

- Running commands before `notebooklm login` → auth errors
- Forgetting `--wait` on generate commands → trying to download before generation finishes
- Using this for notebook/source management — use `notebooklm-mcp-cli` for that
- Expecting `playwright install chromium` only needed once — required after pip updates too
