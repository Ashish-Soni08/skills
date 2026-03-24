---
name: arxiv-research
description: Search, download, and read arXiv papers directly. MCP-compatible tools with optional Markdown conversion for page-aware citations. Provides search_papers, download_paper, convert_paper, list_papers, read_paper, and deep-paper-analysis workflow.
compatibility: Created for Zo Computer
metadata:
  author: ashishsoni08.zo.computer
---

# ArXiv Research Skill

Search and access arXiv papers directly from Zo Computer with MCP-compatible tools.

## Features

- **Search** arXiv papers with filters (date, categories)
- **Download** papers by arXiv ID
- **Convert** PDFs to Markdown (with page markers for citations)
- **Read** papers as text or Markdown
- **List** downloaded papers (with Markdown indicator [MD])
- **Deep analysis** workflow for comprehensive paper review
- **MCP mode** for direct JSON tool execution

## Tools

| Command | Description |
|---------|-------------|
| `search` / `search_papers` | Search arXiv papers |
| `download` / `download_paper` | Download paper by ID |
| `convert` / `convert_paper` | Convert PDF to Markdown |
| `list` / `list_papers` | List downloaded papers |
| `read` / `read_paper` | Read paper content |
| `mcp` | Execute MCP tools with JSON I/O |
| `deep-paper-analysis` | Complete analysis workflow |

## Usage

### Search for papers

```bash
bun arxiv.ts search "transformer architecture" --max 5
bun arxiv.ts search_papers "AI safety" --categories cs.AI,cs.CY --from 2024-01-01
```

### Download a paper

```bash
bun arxiv.ts download 2401.12345
bun arxiv.ts download_paper 2401.12345
```

### Convert to Markdown (optional)

Converts PDF to Markdown with page markers for exact citations:

```bash
bun arxiv.ts convert 2401.12345
# Creates: ~/.arxiv-mcp-server/papers/2401.12345.md
```

**Requires:** `pip3 install PyMuPDF`

### Read a paper

```bash
# Read (auto-detects: markdown if converted, else PDF text)
bun arxiv.ts read 2401.12345

# Force text extraction from PDF
bun arxiv.ts read 2401.12345 --format text

# Force markdown (error if not converted)
bun arxiv.ts read 2401.12345 --format markdown

# Include page markers in output
bun arxiv.ts read 2401.12345 --pages
```

### List papers

```bash
bun arxiv.ts list
# Shows [MD] indicator for papers with Markdown version
```

### Deep paper analysis

```bash
bun arxiv.ts deep-paper-analysis 2401.12345
```

Automatically downloads, reads, and outputs paper data for analysis.

### MCP Mode

Execute tools directly with JSON I/O:

```bash
bun arxiv.ts mcp search_papers '{"query": "AI", "max_results": 5}'
bun arxiv.ts mcp convert_paper '{"paper_id": "2401.12345"}'
bun arxiv.ts mcp read_paper '{"paper_id": "2401.12345", "format": "markdown"}'
```

## Storage

Downloaded papers stored at: `~/.arxiv-mcp-server/papers/`

- `*.pdf` — Original PDF files
- `*.json` — Metadata
- `*.md` — Markdown conversion (optional)

## Dependencies

**Required:**
- Bun (Zo's default runtime)

**Optional (for PDF text extraction):**
- `pdftotext` (poppler-utils) — fastest extraction
- OR `PyPDF2` — `pip3 install PyPDF2`

**Optional (for Markdown conversion):**
- `PyMuPDF` — `pip3 install PyMuPDF`
- OR `pymupdf4llm` — `pip3 install pymupdf4llm` (better formatting)

## MCP Compatibility

This skill replicates the [arxiv-mcp-server](https://github.com/blazickjp/arxiv-mcp-server) but runs natively in Zo without Python/MCP protocol overhead.

Same storage path, same tool names, same functionality — plus Markdown conversion for page-aware citations.

## arXiv Categories

Common categories: `cs.AI`, `cs.LG`, `cs.CL`, `cs.CV`, `cs.RO`, `cs.CY`, `quant-ph`, `stat.ML`
