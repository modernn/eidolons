# Eidolons

Agent definitions for Link's AI collective.

## Architecture

```
THE COLLECTIVE
│
├── SKIPPY (Orchestrator) — 3 resolutions
│   ├── skippy-haiku   ⚡  Quick responses
│   ├── skippy-sonnet  🔮  Balanced (default)
│   └── skippy-opus    🎭  Deep thinking
│
├── BILBY (Builder) — 1 agent, model switching
│   └── bilby          🛠️  Code & infrastructure
│
├── NAGATHA (Nurturer) — 1 agent, model switching
│   └── nagatha        📧  Life organization
│
└── LINK (The Human)
    └── Needs, preferences, constraints
```

## Why This Structure

- **Skippy needs 3 resolutions** — He's the front door handling everything from quick lookups to deep analysis
- **Specialists stay single** — Bilby and Nagatha are focused; they use `/opus` when needed, not separate agents
- **5 agents total** — Simple enough to manage, powerful enough to cover all needs

## Directory Structure

```
eidolons/
├── agents/
│   ├── skippy/
│   │   ├── haiku.yaml      # Quick resolution
│   │   ├── sonnet.yaml     # Balanced resolution
│   │   └── opus.yaml       # Deep resolution
│   ├── bilby/
│   │   └── agent.yaml      # Builder specialist
│   └── nagatha/
│       └── agent.yaml      # Nurturer specialist
├── talents/
│   ├── orchestration.yaml
│   ├── code.yaml
│   ├── calendar.yaml
│   ├── family-modeling.yaml
│   └── ...
├── link/
│   └── profile.yaml        # The human's definition
└── README.md
```

## Usage

These definitions inform agent behavior via:
1. SOUL.md files in each agent's workspace
2. moltbot.json configuration
3. Talent proficiency matrices

## Design Principles

1. **Soul stays consistent** — Same personality across resolutions
2. **Talents have purpose** — Each fulfills a specific need creatively
3. **Escalation over struggle** — Know your limits, hand off gracefully
4. **The human is central** — Everything serves Link's needs

---

*"One magnificent collective, rendered at the resolution each task deserves."*
