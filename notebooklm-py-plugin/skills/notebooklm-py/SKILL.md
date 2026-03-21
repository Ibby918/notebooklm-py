---
name: notebooklm-py
description: Generates content from Google NotebookLM using Python or CLI — quizzes, flashcards, audio podcasts, mind maps, slide decks, and data tables. Use when the user wants to generate or download any of these content types from a notebook.
---

# NotebookLM Python

Full Python API and CLI for NotebookLM content generation. Generates and downloads content
types not available in the web UI (structured quiz JSON, editable PPTX, mind map JSON).

**Authentication required before first use:**
```bash
notebooklm login
```

**Slash command:**
```
/notebooklm
```

## Workflow

### Generate content from an existing notebook

1. Set active notebook:
   ```bash
   notebooklm use <notebook-id>
   ```

2. Generate the desired content type (add `--wait` to block until done):
   ```bash
   notebooklm generate audio --wait
   notebooklm generate quiz --difficulty hard --wait
   notebooklm generate flashcards --quantity more
   notebooklm generate slide-deck --wait
   notebooklm generate mind-map
   notebooklm generate data-table "compare key metrics"
   ```

3. Download the artifact:
   ```bash
   notebooklm download audio ./podcast.mp3
   notebooklm download quiz --format json ./quiz.json
   notebooklm download quiz --format markdown ./quiz.md
   notebooklm download flashcards --format json ./cards.json
   notebooklm download slide-deck ./slides.pdf          # or .pptx
   notebooklm download mind-map ./mindmap.json
   notebooklm download data-table ./data.csv
   ```

### Full pipeline from scratch

```bash
notebooklm create "Study Topic"
notebooklm source add "https://example.com"
notebooklm source add "./paper.pdf"
notebooklm ask "What are the main themes?"
notebooklm generate quiz --difficulty medium --wait
notebooklm download quiz --format json ./quiz.json
```

## Content types and formats

| Type | Download formats | Notes |
|---|---|---|
| Audio | MP3, MP4 | deep-dive / brief / critique / debate |
| Quiz | JSON, Markdown, HTML | configurable difficulty |
| Flashcards | JSON, Markdown, HTML | configurable quantity |
| Slide deck | PDF, **PPTX** | PPTX not available in web UI |
| Mind map | JSON | hierarchical — not in web UI |
| Infographic | PNG | portrait / landscape |
| Data table | CSV | natural language structure prompt |

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
