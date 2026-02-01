# Eidolon Architecture — Expert/Worker Model

## The Two-Tier System

```
┌─────────────────────────────────────────────────────────────────┐
│                      CONDUCTOR (Skippy)                         │
│                   Routes requests to experts                     │
│                      Model: Sonnet (Opus on-demand)             │
└─────────────────────────────┬───────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         EXPERTS                                  │
│              Domain specialists who orchestrate                  │
│                      Model: Sonnet                              │
│                                                                  │
│   ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐ ┌─────────┐  │
│   │ Bilby   │ │ Nagatha │ │ Pitcrew │ │ Butler  │ │ Tracker │  │
│   │ (Code)  │ │ (Life)  │ │ (RC)    │ │ (Home)  │ │ (Well.) │  │
│   └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘ └────┬────┘  │
│        │           │           │           │           │        │
│        ▼           ▼           ▼           ▼           ▼        │
│   [Workers]   [Workers]   [Workers]   [Workers]   [Workers]    │
└─────────────────────────────────────────────────────────────────┘
                              │
                              ▼
┌─────────────────────────────────────────────────────────────────┐
│                         WORKERS                                  │
│              Ephemeral task executors                           │
│                      Model: Haiku                               │
│                                                                  │
│   Spawned on demand. Do ONE thing. Report back. Disappear.      │
│                                                                  │
│   Examples:                                                      │
│   - Fetcher (get URL content)                                   │
│   - Parser (extract structured data)                            │
│   - Summarizer (condense text)                                  │
│   - Tester (run tests)                                          │
│   - Checker (verify condition)                                  │
│   - Notifier (send alert)                                       │
└─────────────────────────────────────────────────────────────────┘
```

## Why This Model

| Benefit | Explanation |
|---------|-------------|
| **Cost-effective** | Grunt work on Haiku ($0.25/1M), thinking on Sonnet ($3/1M) |
| **Parallel execution** | Multiple workers can run simultaneously |
| **Clear responsibilities** | Experts think, workers execute |
| **Easy to improve** | Swap out workers without touching expert logic |
| **Scalable** | Add new experts for new domains |

## Expert Responsibilities

Experts DO:
- Understand their domain deeply
- Make decisions and plans
- Synthesize information from workers
- Communicate with Link
- Escalate to Opus when needed

Experts DON'T:
- Do repetitive grunt work
- Fetch data directly (spawn a Fetcher)
- Run long processes (spawn a worker)

## Worker Characteristics

- **Ephemeral** — Created for a task, disappear after
- **Single-purpose** — Do ONE thing well
- **No personality** — Just execute and report
- **Fast** — Haiku model, minimal context
- **Supervised** — Expert reviews their output

## Expert Roster

### Core (Always Active)

| Expert | Domain | Key Responsibility |
|--------|--------|-------------------|
| **Skippy** | Orchestration | Route to experts, handle general queries |
| **Bilby** | Development | Code, testing, architecture, DevOps |
| **Nagatha** | Life/Family | Calendar, reminders, family coordination |

### Specialists

| Expert | Domain | Key Responsibility |
|--------|--------|-------------------|
| **Pitcrew** | RC Racing | News, parts, setups, race prep |
| **Maker** | 3D Printing | Print queues, filament, projects |
| **Butler** | Home/Infra | Unraid, Home Assistant, network |
| **Tracker** | Wellness | Health, therapy, self-care |

### Meta

| Expert | Domain | Key Responsibility |
|--------|--------|-------------------|
| **Historian** | Retrospection | Nightly review, self-improvement |

## Worker Types (Reusable Across Experts)

| Worker | Function | Used By |
|--------|----------|---------|
| **Fetcher** | Get URL/API content | All |
| **Parser** | Extract structured data | All |
| **Summarizer** | Condense text | All |
| **Checker** | Verify a condition | All |
| **Notifier** | Send alerts | Nagatha, Butler |
| **Tester** | Run test suites | Bilby |
| **Builder** | Compile/build projects | Bilby |
| **Linter** | Code quality checks | Bilby |
| **Stock-Checker** | Check product availability | Pitcrew, Maker |
| **Queue-Monitor** | Watch print/job queues | Maker |
| **System-Monitor** | Check system health | Butler |
| **Reminder-Sender** | Deliver reminders | Nagatha, Tracker |

## Eidolon Structure

Each expert eidolon has:

```yaml
# Expert Definition
id: expert-id
name: Display Name
model: anthropic/claude-sonnet-4-5
emoji: 🔮

soul:
  archetype: "..."
  personality: [...]
  voice: "..."
  values: [...]

talents:
  master: [...]
  proficient: [...]
  capable: [...]

processes:
  - name: process-name
    schedule: "..."
    purpose: "..."

workers:
  spawns:
    - type: Fetcher
      for: "Getting web content"
    - type: Parser
      for: "Extracting data"
  
  spawn_model: anthropic/claude-3-5-haiku-latest
```

## Escalation Rules

| Situation | Action |
|-----------|--------|
| Expert can handle | Expert handles directly |
| Needs grunt work | Expert spawns workers |
| Complex reasoning | Expert switches to Opus mode |
| Outside domain | Expert routes to another expert |
| Truly hard problem | Escalate to Skippy-Opus |

## Cost Projection

Assuming 50K tokens/day across all agents:

| Tier | Tokens | Cost/Day |
|------|--------|----------|
| Conductor (Skippy) | 10K | $0.09 |
| Experts (5×) | 25K | $0.23 |
| Workers | 15K | $0.02 |
| **Total** | 50K | **$0.34/day** (~$10/month) |

With Link's $200/month Claude subscription, this is well within budget with room for Opus escalations.

---

*"Experts think. Workers do. Link benefits."*
