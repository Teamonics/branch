# Claude.md

This file documents how to use Claude (or any LLM) with the Concept Map Generator tool.

## Project Overview

This project is a **Concept Map Generator** - a single-file HTML tool (`index.html`) that transforms LLM-generated JSON into interactive node graphs for visualizing concepts and their relationships.

## How It Works

### User Flow

1. **Enter a topic** - User inputs a subject they want to explore
2. **Copy the prompt** - Tool displays a pre-built prompt template with the topic inserted
3. **Get LLM response** - User pastes the prompt into Claude (or any LLM)
4. **Paste JSON back** - User pastes the LLM's JSON response into the tool
5. **View visualization** - Tool renders an interactive D3.js node graph

### Using with Claude

When you enter a topic, the tool generates a prompt like:

```
Create a concept map for the topic "[YOUR TOPIC]". Return ONLY valid JSON in this exact format:

{
  "topic": "...",
  "nodes": [
    {"id": "1", "label": "...", "layer": 1}
  ],
  "edges": [
    {"from": "1", "to": "2", "type": "hierarchy|dependency|association"}
  ]
}

Generate 10-15 nodes across 3 layers. Use edge types: hierarchy (parent-child), dependency (requires), association (related to).
```

Copy this prompt, paste it into Claude, then paste Claude's JSON response back into the tool.

## JSON Format Specification

```json
{
  "topic": "Your Topic Name",
  "nodes": [
    {"id": "1", "label": "Main Concept", "layer": 1},
    {"id": "2", "label": "Sub Concept", "layer": 2}
  ],
  "edges": [
    {"from": "1", "to": "2", "type": "hierarchy"}
  ]
}
```

**Node properties:**
- `id`: Unique identifier (string)
- `label`: Display text for the node
- `layer`: Vertical position (1-3, top to bottom)

**Edge properties:**
- `from`: Source node ID
- `to`: Target node ID
- `type`: Relationship type
  - `hierarchy` - Parent-child relationship (blue)
  - `dependency` - Requirement/dependency (orange)
  - `association` - General relationship (gray)

## Visualization Features

- **D3.js powered** - Uses D3.js from CDN for graph rendering
- **Layer-based layout** - 3 layers positioned top-to-bottom
- **Color-coded edges** - Visual distinction between relationship types
- **Draggable nodes** - Interactive repositioning
- **Node labels** - Clear text labels on each node
- **Responsive design** - Mobile-friendly interface

## Technical Details

- **Single-file architecture** - All HTML, CSS, and JavaScript in `index.html`
- **No build process** - Open directly in browser
- **CDN dependencies** - D3.js loaded from CDN
- **Clean, modern UI** - Minimal, user-friendly interface

## Tips for Best Results

1. **Be specific with topics** - More focused topics generate better maps
2. **Review the JSON** - Check that the LLM output is valid JSON before pasting
3. **Iterate** - Try different prompts to get different perspectives
4. **Save outputs** - Copy the JSON to reuse interesting concept maps

## Compatible LLMs

This tool works with any LLM that can generate structured JSON:
- Claude (Anthropic)
- GPT-4 (OpenAI)
- Gemini (Google)
- Or any other LLM with JSON output capabilities
