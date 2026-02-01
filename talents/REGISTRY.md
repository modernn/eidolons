# Talent Registry

*Living inventory of what we can actually do — updated as we learn.*

## How This Works

When an agent successfully uses a capability:
1. Check if it's documented here
2. If not → add it with real observations
3. If yes → update with learnings (gotchas, cost, reliability)

**Format for each talent:**
```yaml
talent-name:
  status: proven | experimental | broken
  agents: [who uses this]
  implementation: how it actually works
  cost: rough estimate (tokens, API calls, time)
  reliability: 0-10
  gotchas: things that trip us up
  last_used: date
  notes: real-world observations
```

---

## Proven Talents (we know these work)

### gateway-migration
- **Status:** proven
- **Agents:** [skippy]
- **Implementation:** rsync + config export/import
- **What we learned (2026-02-01):**
  - Need SSH keys authorized between servers
  - Config paths must be updated for new username
  - Can't run two gateways on same Telegram bots

### sub-agent-spawning
- **Status:** proven
- **Agents:** [skippy, nagatha, bilby]
- **Implementation:** sessions_spawn tool
- **Cost:** Haiku for workers, Sonnet for complex tasks
- **What we learned:**
  - Great for parallel independent work
  - Results come back async via announce
  - Can spawn multiple simultaneously

### git-repo-management
- **Status:** proven
- **Agents:** [skippy, bilby]
- **Implementation:** exec + git CLI
- **Reliability:** 10
- **Notes:** Push to GitHub works seamlessly

### yaml-domain-design
- **Status:** proven
- **Agents:** [skippy, nagatha]
- **Implementation:** Write tool + YAML formatting
- **What we learned (2026-02-01):**
  - Sub-agents can write comprehensive domain files
  - ~700-800 lines per domain is typical
  - Pattern works well for expert/worker hierarchies

---

## Experimental Talents (trying these out)

### mcp-calendar (Skylight)
- **Status:** experimental
- **Agents:** [nagatha]
- **Implementation:** Skylight MCP → ProtonMail
- **Gotchas:** 
  - MCP server needs to be running
  - Auth tokens can expire
- **Last tested:** 2026-01-29
- **Notes:** Was working, needs verification on new server

### browser-control
- **Status:** experimental
- **Agents:** [skippy]
- **Implementation:** browser tool via node proxy
- **Reliability:** varies by node connection
- **Gotchas:**
  - Nodes need to be online
  - Some sites block automation

---

## Planned Talents (not yet implemented)

### unraid-management
- **Implementation:** Unraid MCP (jmagar/unraid-mcp)
- **Status:** planned
- **Blocked by:** MCP server deployment

### home-assistant-control
- **Implementation:** HA skill or MCP
- **Status:** planned
- **Blocked by:** Dell node setup, HA integration

### email-management (Gmail)
- **Implementation:** gog CLI
- **Status:** planned
- **Gotchas to watch:** OAuth setup

---

## Broken/Deprecated Talents

*(Move things here when they stop working)*

---

## Talent Discovery Log

| Date | Talent | Agent | Outcome | Notes |
|------|--------|-------|---------|-------|
| 2026-02-01 | gateway-migration | skippy | success | Migrated to new Proxmox VM |
| 2026-02-01 | domain-design | nagatha | success | Created 5 life/family experts |
| 2026-02-01 | parallel-spawning | skippy | success | 3 domain designs simultaneously |

---

*Add entries as we learn. This is our collective memory of what actually works.*
