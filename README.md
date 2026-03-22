# RoadMem — Sovereign Agent Memory

> Forked from [mem0](https://github.com/mem0ai/mem0). Customized for BlackRoad OS agent fleet.

**RoadMem** gives every BlackRoad agent persistent memory — hybrid vector + graph storage that's 26% better than OpenAI's memory at context retrieval.

## Features

- **Hybrid storage**: Vector (Qdrant on Alice) + Graph (knowledge graph in SQLite)
- **Per-agent memory**: Each of 35 agents has its own memory namespace
- **Cross-session**: Agents remember conversations across restarts
- **Semantic search**: Find relevant memories by meaning, not just keywords
- **Fleet-distributed**: Memory syncs across Pi nodes via NATS (CarPool)

## Architecture

```
Agent → RoadMem API → Qdrant (vectors) + SQLite (graph)
                    → NATS (CarPool) → Fleet sync
                    → RoadChain (audit log)
```

## Quick Start

```bash
pip install -r requirements.txt
export QDRANT_URL=http://192.168.4.49:6333
export OLLAMA_URL=http://192.168.4.96:11434
python -m roadmem serve --port 8901
```

## BlackRoad Integration

- **Qdrant**: Vector DB on Alice (192.168.4.49:6333)
- **Ollama**: Embeddings via nomic-embed-text on Cecilia
- **NATS**: Memory sync via CarPool on Octavia
- **RoadChain**: Every memory write logged to immutable ledger

---

© 2026 BlackRoad OS, Inc. Fork of mem0 (Apache 2.0). BlackRoad customizations proprietary.
