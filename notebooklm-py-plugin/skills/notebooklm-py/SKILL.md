---
name: notebooklm-py
description: Python API and CLI for Google NotebookLM. Use when the user wants to generate podcasts, quizzes, flashcards, mind maps, slide decks or data tables from NotebookLM notebooks via Python or CLI.
---

# NotebookLM Python — Full Python API for Google NotebookLM

Comprehensive Python API and CLI for NotebookLM. Generate audio, video, quizzes, flashcards, mind maps and more. Includes features not available in the web UI.

## When to Use This Skill

- User wants to generate content from NotebookLM (podcasts, quizzes, flashcards)
- User wants to download artifacts from NotebookLM
- User wants to automate NotebookLM workflows with Python
- User says "generate a quiz from my notebook" or "make flashcards for this"

## Setup Requirement

```bash
pip install "notebooklm-py[browser]"
playwright install chromium
notebooklm login    # Authenticate with Google account
```

## CLI Usage

```bash
# Create notebook and add sources
notebooklm create "My Research"
notebooklm source add "https://example.com"
notebooklm source add "./paper.pdf"

# Chat with sources
notebooklm ask "What are the key themes?"

# Generate content
notebooklm generate audio --wait
notebooklm generate quiz --difficulty hard
notebooklm generate flashcards --quantity more
notebooklm generate slide-deck
notebooklm generate mind-map
notebooklm generate data-table "compare key concepts"

# Download artifacts
notebooklm download audio ./podcast.mp3
notebooklm download quiz --format json ./quiz.json
notebooklm download flashcards --format markdown ./cards.md
notebooklm download mind-map ./mindmap.json
notebooklm download slide-deck ./slides.pdf
```

## Claude Code Slash Command

```bash
/notebooklm    # Activate NotebookLM skill
```

## Content Generation Options

| Type | Formats |
|---|---|
| Audio Overview | deep-dive, brief, critique, debate |
| Quiz | JSON, Markdown, HTML |
| Flashcards | JSON, Markdown, HTML |
| Slide Deck | PDF, PPTX |
| Mind Map | JSON |
| Data Table | CSV |

## Trading Use Cases

- Generate flashcards from trading strategy documentation
- Create a quiz to test your knowledge of chart patterns
- Build mind maps from research reports
- Generate podcasts from earnings transcripts for commute listening
