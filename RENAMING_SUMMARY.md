# Umbenennung: Kylo Note → Obsidian Agent

**Datum**: 2026-02-17
**Status**: ✅ Dokumentation aktualisiert, Projektstruktur ausstehend

---

## Änderungsübersicht

### 1. Produktname
- **Alt**: Kylo Note
- **Neu**: Obsidian Agent
- **Begründung**: Klarere Positionierung als agentische Betriebsschicht für Obsidian

### 2. Technische Namenskonventionen

#### Verzeichnisstruktur (intern)
```diff
- .kylonote/
- .kilonote/  (inkonsistente Schreibweise bereinigt)
+ .obsidian-agent/
```

**Unterverzeichnisse:**
```
.obsidian-agent/
├── checkpoints/     # Shadow Git Repo für Restore Points
├── index/          # Semantic Index Storage
└── skills/         # User-defined Workflow Skills
```

#### Ignore File
```diff
- .kylonoteignore
+ .obsidianagentignore
```

#### Package/Module Namen
```diff
- kylo-note
- kylonote
+ obsidian-agent
```

---

## Aktualisierte Dateien

### Core Dokumentation (✅ Fertig)
- [x] `context/01_product-vision.md`
- [x] `context/02_capability-scope.md`
- [x] `context/03_research-findings.md`
- [x] `context/05_constraints-nfrs.md`
- [x] `context/08_deep-research-consolidated.md`

### Requirements (✅ Fertig)
- [x] `requirements/overview.md`
- [x] `requirements/handoff/re-to-architect.md`
- [x] `requirements/gap_analysis_log.md`
- [x] `requirements/epics/*.md`
- [x] `requirements/features/*.md` (alle 13 Feature-Specs)

### Business/Docs (✅ Fertig)
- [x] `docs/business-analysis.md`
- [x] `.kilocode/rules/memory-bank/coding-brief.md`

---

## Noch ausstehende Änderungen

### 1. Projektverzeichnis umbenennen
```bash
cd /Users/sebastianhanke/projects
mv kylonote obsidian-agent
```

### 2. Package Configuration erstellen

**`package.json`** (Obsidian Plugin):
```json
{
  "name": "obsidian-agent",
  "version": "0.1.0",
  "description": "Agentic operating layer for Obsidian - Kilo Code for knowledge work",
  "main": "main.js",
  "scripts": {
    "dev": "esbuild src/main.ts --bundle --external:obsidian --outfile=main.js --watch",
    "build": "esbuild src/main.ts --bundle --external:obsidian --outfile=main.js --minify"
  },
  "keywords": ["obsidian", "plugin", "agent", "ai", "llm", "mcp"],
  "author": "Sebastian Hanke",
  "license": "Apache-2.0"
}
```

**`manifest.json`** (Obsidian Plugin Manifest):
```json
{
  "id": "obsidian-agent",
  "name": "Obsidian Agent",
  "version": "0.1.0",
  "minAppVersion": "1.4.0",
  "description": "Agentic operating layer for Obsidian with approval-based vault operations, MCP support, and local checkpoints",
  "author": "Sebastian Hanke",
  "authorUrl": "https://github.com/yourusername/obsidian-agent",
  "isDesktopOnly": true
}
```

### 3. Forked Kilo Code Reference
Das Verzeichnis `forked-kilocode/` kann erstmal so bleiben als Referenz.
Später bei der Implementation wird der relevante Code direkt nach `src/` portiert.

### 4. Git Repository
```bash
cd /Users/sebastianhanke/projects/obsidian-agent
git remote set-url origin https://github.com/yourusername/obsidian-agent.git
git commit -am "Rename project: Kylo Note → Obsidian Agent"
```

---

## Naming Patterns für Code

### Module/Classes
```typescript
// Provider
class ObsidianAgentProvider extends ItemView { }

// Settings
interface ObsidianAgentSettings { }

// Services
class MarkdownAutocompleteManager { }
class CheckpointService { }
class SemanticIndexService { }
```

### File Structure (zukünftig)
```
obsidian-agent/
├── src/
│   ├── main.ts                    # Plugin Entry Point
│   ├── provider/
│   │   └── ObsidianAgentProvider.ts
│   ├── services/
│   │   ├── markdown-autocomplete/
│   │   ├── checkpoints/
│   │   ├── semantic-index/
│   │   ├── mcp/
│   │   └── skills/
│   ├── adapters/
│   │   └── obsidian-api.ts
│   └── ui/
│       └── components/
├── packages/
│   ├── types/
│   ├── core-schemas/
│   └── agent-runtime/
├── manifest.json
├── package.json
└── README.md
```

---

## User-Facing Namen

### Plugin Name in Obsidian
- **Display Name**: "Obsidian Agent"
- **Command Palette Prefix**: "Obsidian Agent: ..."
- **Settings Tab Title**: "Obsidian Agent"

### Documentation
- **GitHub Repo**: `obsidian-agent`
- **Plugin ID**: `obsidian-agent`
- **Community Plugin Listing**: "Obsidian Agent - Agentic Operating Layer"

---

## Zusammenfassung

| Kategorie | Alt | Neu | Status |
|-----------|-----|-----|--------|
| Produktname | Kylo Note | Obsidian Agent | ✅ |
| Verzeichnisse | `.kylonote/`, `.kilonote/` | `.obsidian-agent/` | ✅ (Docs) |
| Ignore File | `.kylonoteignore` | `.obsidianagentignore` | ✅ (Docs) |
| Package Name | `kylo-note` | `obsidian-agent` | ⏳ (bei Init) |
| Projektverzeichnis | `/projects/kylonote` | `/projects/obsidian-agent` | ⏳ |
| Plugin ID | - | `obsidian-agent` | ⏳ (bei Init) |

---

## Nächste Schritte

1. **Projektverzeichnis umbenennen** (optional, aber empfohlen)
2. **Plugin Boilerplate erstellen** mit neuen Namen
3. **Architecture Phase starten** mit aktualisierten Requirements

Die Dokumentation ist jetzt konsistent und bereit für die Architektur-Phase.
