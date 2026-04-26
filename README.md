# open-bim-ai-stack

> Vendor-independent BIM workflows powered by LLMs over open standards.

A curated collection of configurations, scripts, and examples for controlling BIM and 3D architecture software through large language models (Claude, Cursor, etc.) via the Model Context Protocol (MCP) — using **exclusively open formats**. No Autodesk dependency. No proprietary lock-in.

---

*The `.rvt` format is the trap. The `.ifc` standard is the exit. AI is the timing.*

---

## Why this exists

The AEC industry has been hostage to proprietary BIM ecosystems for two decades. Autodesk AEC Collection costs ~€3,600/seat/year. An `.rvt` file only opens in Revit. Meanwhile, the EU BIM Mandate was built on IFC — an open ISO standard — not on Revit.

Open BIM tools like Bonsai have had a production-grade IFC engine for years. What held them back was not capability — it was UX. Blender is a tool built for 3D generalists, not architects. The interface friction was the blocker.

> **Bonsai's IFC engine is already production-grade. The missing piece was a usable interface for architects. That piece is now an LLM away.**

The MCP moment changes the equation. LLMs can now reason about building models and act on them through a standardized interface. "Give me a ground floor plan with door tags and dimensions" becomes a prompt, not a menu hunt. The interface friction that blocked open BIM adoption for a decade is solvable with a language model.

This repo maps that path and assembles the pieces into a coherent, opinionated workflow.

## Architecture

```
Claude / Cursor  →  MCP (stdio)  →  MCP4IFC / Bonsai MCP  →  IfcOpenShell  →  .ifc (native)
```

No proprietary middleware. The model lives in IFC from the first element. Any IFC-compliant viewer or authoring tool can open it.

## What's included

- **MCP configs** — ready-to-use `mcp.json` for Claude Desktop, Claude Code and Cursor targeting IFC, Rhino and SketchUp
- **IfcOpenShell scripts** — Python automations on IFC files without opening any GUI
- **Bonsai setup guide** — native IFC authoring in Blender with MCP bridge
- **RhinoAI MCP** — Claude ↔ Rhino/Grasshopper bridge for parametric design
- **SketchUp MCP** — SketchUp control via Python server + Ruby plugin
- **IFC Git workflow** — version-control your BIM model like source code
- **Prompt library** — tested prompts for common BIM tasks in natural language

## Stack

| Layer | Tool |
|---|---|
| IFC engine | Bonsai (Blender) — native IFC authoring, no translation layer |
| AI as UX | MCP + LLM replace GUI friction for architects |
| Format | IFC (ISO 16739) — never `.rvt`, never `.pln` |
| IFC library | IfcOpenShell (Python) |
| AI protocol | Model Context Protocol (MCP) |
| AI clients | Claude Desktop · Claude Code · Cursor · Windsurf |
| Parametric | Rhino 8 + Grasshopper · RhinoAI MCP |
| 2D docs | Bonsai drawings → Inkscape *(gap being actively closed)* |
| Versioning | IFC Git — git-based model version control |

## Quick start

```bash
git clone https://github.com/yourusername/open-bim-ai-stack
cd open-bim-ai-stack
pip install ifcopenshell
cp configs/claude_desktop.json ~/.config/claude/mcp.json
```

Open Claude Desktop. Describe a building element. It appears in your IFC model.

## Status

This is a roadmap and a stake in the ground, not a finished toolkit.  
If you're building in this space, open an issue or get in touch.

- [x] Landscape docs and related projects — Apr 2026
- [ ] Claude Desktop MCP configs for IFC
- [ ] IfcOpenShell script examples
- [ ] Bonsai setup guide + MCP bridge
- [ ] Prompt library for common architectural tasks
- [ ] IFC Git workflow documentation

## Related projects

*Ordered roughly by relevance to this repo's goals.*

### [show2instruct/mcp4ifc](https://arxiv.org/abs/2511.05533)
The most complete open MCP server for IFC to date. 50+ BIM tools, RAG-based dynamic code generation, built on IfcOpenShell + Bonsai. Academic origin but fully open source and functional. This repo builds directly on top of their architecture.

### [JotaDeRodriguez/Bonsai_mcp](https://github.com/JotaDeRodriguez/Bonsai_mcp)
Fork of BlenderMCP extending it with dedicated IFC support via Bonsai. 11 IFC-specific tools for querying projects, listing entities, exploring spatial structure and analysing relationships. MIT licensed, Dockerized, and the author is actively looking for collaborators. The closest thing to a ready-made Claude ↔ Bonsai bridge.

### [louistrue](https://github.com/louistrue)
The closest match in spirit. Independent developer building open tools for sustainable construction and BIM automation: MCP server for IFC5/IFCX authoring, LLM-driven LCA calculators, multi-agent pipeline that takes an address and produces a full IFC model with structural, MEP and facade review loops.

### [dcy0577/Text2BIM](https://github.com/dcy0577/Text2BIM)
Multi-agent LLM framework for generating IFC building models from natural language, with a Vectorworks integration and Solibri model checker in the loop. Good reference for agentic BIM workflows even if the authoring tool is proprietary.

### [Modular Reference Architecture for MCP-BIM Servers](https://arxiv.org/abs/2601.00809)
Recent paper proposing a microservice architecture that decouples the MCP interface from any specific BIM API — solving the portability problem that makes current implementations ad hoc and hard to reuse. Prototype built on IfcOpenShell. Essential reading for anyone designing an MCP server in this space.

### [smartaec/ifcMCP](https://github.com/smartaec/ifcMCP)
Minimal MCP server for querying IFC files. Early-stage but clean architecture. Good starting point if you want to understand the IFC ↔ MCP interface at its simplest.

### [opensourceBIM collective](https://github.com/opensourceBIM)
69 repositories of IFC infrastructure: BIMserver, viewers, plugins, validators. The bedrock of open BIM tooling. No AI integration yet, but essential context for anyone working with IFC at scale.

### [IfcOpenShell](https://ifcopenshell.org)
The common denominator of the entire open BIM ecosystem. The Python library that reads, writes and manipulates IFC natively. Every project listed above depends on it. So does this one.  
→ [github.com/IfcOpenShell/IfcOpenShell](https://github.com/IfcOpenShell/IfcOpenShell)
