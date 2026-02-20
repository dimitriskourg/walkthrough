# Walkthrough: How the Walkthrough Skill Works

> The walkthrough skill turns a plain-English prompt into a Markdown document with an embedded Mermaid diagram of your codebase. The AI agent reads the skill definition, launches parallel subagents to explore relevant code, synthesizes findings, and outputs a self-contained `.md` file with a diagram, reference table, and prose explanation.

## Diagram

```mermaid
graph TD
  %% --- Subgroup: Trigger ---
  subgraph trigger["Trigger"]
    userPrompt(["<b>User Prompt</b><br/><i>The natural-language request that kicks off the walkthrough.<br/>Matches phrases like 'walkthrough', 'explain this flow', 'how does X work'.</i>"])
  end

  %% --- Subgroup: Skill Configuration ---
  subgraph skill_config["Skill Configuration"]
    skillDefinition["<b>Skill Definition</b><br/><i>Defines the four-step workflow: understand scope,<br/>explore with subagents, choose diagram type, generate .md file.</i>"]
  end

  %% --- Subgroup: Exploration Phase ---
  subgraph exploration["Exploration Phase"]
    scopeUnderstanding["<b>Scope Understanding</b><br/><i>Clarifies what the user wants explained and frames it<br/>as a mental model with 5-12 key concepts.</i>"]
    parallelExploration["<b>Parallel Subagents</b><br/><i>Launches 2-4 Explore subagents via the Task tool.<br/>Each investigates one area and returns a structured report.</i>"]
    synthesis["<b>Synthesis</b><br/><i>Combines subagent findings into node list, edge list,<br/>and subgraph groupings. Targets 5-12 nodes total.</i>"]
  end

  %% --- Subgroup: Generation Phase ---
  subgraph generation["Generation Phase"]
    diagramSelection["<b>Diagram Selection</b><br/><i>Picks flowchart (graph TD/LR) for feature flows<br/>or ER diagram for database schemas.</i>"]
    markdownOutput["<b>Markdown Output</b><br/><i>Writes a single .md file with an embedded Mermaid diagram,<br/>Key Concepts table, and prose explanation.</i>"]
  end

  %% --- Subgroup: Result ---
  subgraph result["Result"]
    walkthroughFile(["<b>Walkthrough File</b><br/><i>A self-contained .md file that renders on GitHub,<br/>VS Code, and any Markdown viewer with Mermaid support.</i>"])
  end

  %% --- Edges ---
  userPrompt -->|"triggers"| scopeUnderstanding
  skillDefinition -.->|"guides"| scopeUnderstanding
  scopeUnderstanding -->|"defines areas"| parallelExploration
  parallelExploration -->|"reports findings"| synthesis
  synthesis -->|"feeds concepts"| diagramSelection
  diagramSelection -->|"produces"| markdownOutput
  markdownOutput -->|"writes"| walkthroughFile

  %% --- Node type styles ---
  classDef component fill:#a855f7,stroke:#c084fc,color:#fff
  classDef composable fill:#7c3aed,stroke:#a78bfa,color:#fff
  classDef utility fill:#6d28d9,stroke:#8b5cf6,color:#fff
  classDef external fill:#525252,stroke:#737373,color:#fff
  classDef event fill:#d8b4fe,stroke:#e9d5ff,color:#000
  classDef data fill:#9333ea,stroke:#a855f7,color:#fff

  %% --- Node type assignments ---
  class userPrompt event
  class skillDefinition data
  class scopeUnderstanding utility
  class parallelExploration composable
  class synthesis utility
  class diagramSelection utility
  class markdownOutput component
  class walkthroughFile component
```

## Key Concepts

| Concept | Description | File(s) |
|---------|-------------|---------|
| **User Prompt** | The natural-language request that kicks off the walkthrough. Matches phrases like "walkthrough", "explain this flow", "how does X work". | `skills/walkthrough/skill.md:1-3` |
| **Skill Definition** | Defines the four-step workflow: understand scope, explore with subagents, choose diagram type, generate .md file. | `skills/walkthrough/skill.md` |
| **Scope Understanding** | Clarifies what the user wants explained and frames it as a mental model with 5-12 key concepts. | `skills/walkthrough/skill.md:25-35` |
| **Parallel Subagents** | Launches 2-4 Explore subagents via the Task tool. Each investigates one area and returns a structured report. | `skills/walkthrough/skill.md:37-88` |
| **Synthesis** | Combines subagent findings into node list, edge list, and subgraph groupings. Targets 5-12 nodes total. | `skills/walkthrough/skill.md:90-100` |
| **Diagram Selection** | Picks flowchart (graph TD/LR) for feature flows or ER diagram for database schemas. | `skills/walkthrough/skill.md:102-170` |
| **Markdown Output** | Writes a single .md file with an embedded Mermaid diagram, Key Concepts table, and prose explanation. | `skills/walkthrough/skill.md:172-240` |
| **Walkthrough File** | A self-contained .md file that renders on GitHub, VS Code, and any Markdown viewer with Mermaid support. | `walkthrough-*.md` |

## How It Connects

The process starts when a user writes a natural-language prompt asking to understand part of a codebase. The skill definition guides the agent through a four-step workflow. First, the agent clarifies the scope and frames the request as a mental model with 5-12 key concepts. Then it launches parallel Explore subagents to investigate different areas of the codebase, and synthesizes their findings into a structured list of nodes, edges, and groupings. Finally, the agent selects the appropriate diagram type and generates a Markdown file containing the Mermaid diagram, a Key Concepts reference table, and a prose explanation of how everything connects.
