---
name: notebooklm-py
description: >
  Use this skill whenever the user wants to generate content from Google NotebookLM using
  Python or the notebooklm CLI — specifically audio podcasts, quizzes, flashcards, mind maps,
  slide decks, infographics, or data tables. Trigger for requests like "generate a quiz from
  my notebook", "make flashcards from this content", "create a podcast overview", "download
  the quiz as JSON", "generate a mind map", or "create a slide deck from my research". Also
  trigger for Python-based NotebookLM automation workflows. Prefer this skill over
  notebooklm-mcp-cli when the user wants content generation and downloads specifically.
  Use notebooklm-mcp-cli for notebook/source management. Skip for general NotebookLM UI
  questions. Skip if the user just wants to query a notebook — nlm query handles that.
  Note: requires notebooklm login authentication before first use.
---

# NotebookLM Python — Full Python API for Google NotebookLM

Comprehensive Python API and CLI with features beyond the NotebookLM web UI. Generate audio,
video, quizzes, flashcards, mind maps, slide decks and data tables — and download them locally.

## Prerequisites

```bash
pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login    # Authenticate with Google account
```

## Quick Start CLI

```bash
# Create notebook and add sources
notebooklm create "My Research Topic"
notebooklm source add "https://example.com/article"
notebooklm source add "./research-paper.pdf"

# Ask questions
notebooklm ask "What are the main conclusions?"

# Generate content (all require --wait to block until done)
notebooklm generate audio --wait                    # Podcast overview
notebooklm generate quiz --difficulty hard --wait   # Quiz
notebooklm generate flashcards --quantity more      # Flashcards
notebooklm generate slide-deck --wait               # Slide deck
notebooklm generate mind-map                        # Mind map
notebooklm generate infographic --orientation portrait
notebooklm generate data-table "compare key metrics"

# Download artifacts
notebooklm download audio ./podcast.mp3
notebooklm download quiz --format json ./quiz.json
notebooklm download quiz --format markdown ./quiz.md
notebooklm download flashcards --format json ./cards.json
notebooklm download slide-deck ./slides.pdf          # or .pptx
notebooklm download mind-map ./mindmap.json
notebooklm download data-table ./data.csv
```

## Content Generation Options

| Type | Format Options | Notes |
|---|---|---|
| Audio Overview | deep-dive, brief, critique, debate | MP3/MP4 |
| Video Overview | classic, whiteboard, kawaii, anime | MP4 |
| Quiz | JSON, Markdown, HTML | Configurable difficulty |
| Flashcards | JSON, Markdown, HTML | Configurable quantity |
| Slide Deck | PDF, **PPTX** (editable) | Not available in web UI |
| Mind Map | JSON (hierarchical) | Not available in web UI |
| Infographic | portrait, landscape | PNG |
| Data Table | CSV | Custom structure via prompt |

## Features Not in the Web UI

These are only available via this tool:
- Download quiz/flashcard data as structured JSON for your own apps
- Export mind map as JSON for custom visualisation
- Download slide decks as editable PPTX (not just PDF)
- Batch download all artifacts of a type at once
- Save chat answers as notebook notes

## Trading & Study Workflows

**Generate study materials from strategy docs:**
```bash
notebooklm create "Trading Strategy Notes"
notebooklm source add "./parity-engine-docs.md"
notebooklm generate quiz --difficulty medium --wait
notebooklm download quiz --format json ./strategy-quiz.json
notebooklm generate flashcards --quantity more
notebooklm download flashcards --format markdown ./flashcards.md
```

**Research podcast for commute:**
```bash
notebooklm generate audio --wait  # deep-dive format
notebooklm download audio ./morning-brief.mp3
```

## Python API

```python
import asyncio
from notebooklm import NotebookLMClient

async def main():
    async with await NotebookLMClient.from_storage() as client:
        nb = await client.notebooks.create("Research")
        await client.sources.add_url(nb.id, "https://example.com")
        status = await client.artifacts.generate_quiz(nb.id)
        await client.artifacts.wait_for_completion(nb.id, status.task_id)
        await client.artifacts.download_quiz(nb.id, "quiz.json", output_format="json")

asyncio.run(main())
```

## Slash Command

```
/notebooklm    # Activate the NotebookLM skill in Claude Code
```
