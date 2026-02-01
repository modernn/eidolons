# Eidolons

Agent definitions for Link's AI collective.

## The Three-Part Model

Each eidolon consists of:

```
EIDOLON
├── SOUL       → Who they are (identity, personality, values)
├── TALENTS    → What makes them good at things (capabilities + proficiency)
└── PROCESSES  → Mental routines that run regularly (recurring thoughts/actions)
```

**Soul** is static — it's who the agent *is*.  
**Talents** are capabilities — what they're *good at*.  
**Processes** are dynamic — what they *do* regularly without being asked.

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

## Directory Structure

```
eidolons/
├── agents/                    # SOULS
│   ├── skippy/
│   │   ├── haiku.yaml         # Quick resolution
│   │   ├── sonnet.yaml        # Balanced resolution
│   │   └── opus.yaml          # Deep resolution
│   ├── bilby/
│   │   └── agent.yaml         # Builder specialist
│   └── nagatha/
│       └── agent.yaml         # Nurturer specialist
│
├── talents/                   # CAPABILITIES
│   ├── orchestration.yaml     # Route tasks
│   ├── code.yaml              # Write software
│   ├── calendar.yaml          # Manage schedules
│   ├── family-modeling.yaml   # Understand perspectives
│   ├── research.yaml          # Find information
│   └── reminders.yaml         # Don't forget things
│
├── processes/                 # MENTAL ROUTINES
│   ├── nightly-retrospective.yaml   # Self-improvement (3:30 AM)
│   ├── morning-briefing.yaml        # Day prep (7:30 AM AK)
│   ├── heartbeat-check.yaml         # Proactive monitoring (30m)
│   ├── memory-consolidation.yaml    # Memory health (weekly)
│   ├── calendar-conflict-scan.yaml  # Schedule checking (hourly)
│   └── project-status.yaml          # LapForge health (daily)
│
├── link/
│   └── profile.yaml           # The human's definition
│
└── README.md
```

## Processes Overview

| Process | Owner | Schedule | Purpose |
|---------|-------|----------|---------|
| Nightly Retrospective | Skippy | 3:30 AM UTC | Self-improvement |
| Morning Briefing | Nagatha | 7:30 AM AK | Start Link's day |
| Heartbeat Check | Skippy | Every 30m | Proactive monitoring |
| Memory Consolidation | Skippy | Weekly (Sun) | Keep memory healthy |
| Calendar Conflict Scan | Nagatha | Hourly | Catch scheduling issues |
| Project Status | Bilby | Weekdays 9am | LapForge health |

## Design Principles

1. **Soul stays consistent** — Same personality across resolutions
2. **Talents have purpose** — Each fulfills a specific need creatively
3. **Processes are proactive** — Don't wait to be asked
4. **Escalation over struggle** — Know your limits, hand off gracefully
5. **The human is central** — Everything serves Link's needs

## Usage

These definitions inform agent behavior via:
1. SOUL.md files in each agent's workspace
2. moltbot.json configuration
3. Cron jobs for processes
4. Talent proficiency routing

---

*"One magnificent collective, thinking even when you're not asking."*
