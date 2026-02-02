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
  - Export `~/.moltbot/` and `~/clawd/` as tarballs, restore on new server

### sub-agent-spawning
- **Status:** proven
- **Agents:** [skippy, nagatha, bilby]
- **Implementation:** sessions_spawn tool
- **Cost:** Haiku for workers, Sonnet for complex tasks
- **Reliability:** 9
- **What we learned:**
  - Great for parallel independent work
  - Results come back async via announce
  - Can spawn multiple simultaneously
  - Used successfully for domain design (3 agents in parallel)

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
  - Created 5 domains, 15 experts, ~50 workers in one session

### node-pairing
- **Status:** proven
- **Agents:** [skippy]
- **Implementation:** nodes tool + moltbot-node CLI
- **What we learned (2026-01-30):**
  - Windows and Linux nodes both work
  - OpenClaw uses `OPENCLAW_GATEWAY_TOKEN` env var (not `CLAWDBOT_GATEWAY_TOKEN`)
  - `gateway.bind: "tailnet"` needs full gateway restart to take effect
  - Nodes provide: browser proxy, system.run capabilities
- **Gotchas:**
  - Node must be online to use
  - Gateway restart required after bind config changes

### proxmox-vm-scripting
- **Status:** proven
- **Agents:** [skippy]
- **Implementation:** bash scripts with qm commands
- **What we learned (2026-01-30):**
  - OVH servers often have `local` (dir) storage, not `local-lvm`
  - Directory storage needs `format=qcow2` in disk creation
  - Ubuntu version URLs change (24.04.2 → 24.04.1) — always verify
  - Check `pvesm status` before scripting to get storage name
- **Gotchas:**
  - Ubuntu ISO URLs get stale (check releases.ubuntu.com)
  - Storage type affects qm disk syntax
  - Old ISOs redirect to old-releases.ubuntu.com

### cron-job-configuration
- **Status:** proven
- **Agents:** [skippy]
- **Implementation:** moltbot cron commands
- **What we learned (2026-01-30):**
  - `sessionTarget: "main"` + `systemEvent` = messages queued but never processed
  - `sessionTarget: "isolated"` + `agentTurn` = actually runs an agent
  - Jobs running in 4-7ms are NOT doing real work — that's just event queuing
  - Need `agentTurn` to spawn actual agent sessions
- **Critical gotcha:** If your cron job runs in milliseconds, it's broken!

### infrastructure-documentation
- **Status:** proven  
- **Agents:** [skippy]
- **Implementation:** memory files + MEMORY.md
- **What we learned:**
  - Daily files (`memory/YYYY-MM-DD.md`) for raw session notes
  - `MEMORY.md` for curated long-term context
  - auto-capture creates noise — periodic cleanup helps

---

## Experimental Talents (trying these out)

### mcp-calendar (Skylight)
- **Status:** experimental
- **Agents:** [nagatha]
- **Implementation:** Skylight MCP → ProtonMail
- **Gotchas:** 
  - MCP server needs to be running
  - Auth tokens can expire
  - SIGKILL errors seen when process times out
- **Last tested:** 2026-01-29
- **Notes:** Login works but commands can hang/timeout

### browser-control
- **Status:** experimental
- **Agents:** [skippy]
- **Implementation:** browser tool via node proxy
- **Reliability:** varies by node connection
- **Gotchas:**
  - Nodes need to be online
  - Some sites block automation
  - Chrome extension relay requires user to attach tab

### vm-os-selection
- **Status:** experimental
- **Agents:** [skippy]
- **Implementation:** OVH panel + custom scripts
- **What we learned (2026-01-30):**
  - Proxmox > bare metal Ubuntu for flexibility
  - HAOS VM is best way to run Home Assistant
  - Nextcloud works well as LXC container
  - WAN Proxmox clustering (OVH ↔ home) is finicky — avoid unless needed

---

## Planned Talents (not yet implemented)

### unraid-management
- **Implementation:** Unraid MCP (jmagar/unraid-mcp)
- **Status:** planned
- **Blocked by:** MCP server deployment
- **Note:** Link considering switching Unraid box to Proxmox anyway

### home-assistant-control
- **Implementation:** HA skill or MCP
- **Status:** planned
- **Blocked by:** HAOS VM deployment on OVH Proxmox

### email-management (Gmail)
- **Implementation:** gog CLI
- **Status:** planned
- **Gotchas to watch:** OAuth setup

### nextcloud-integration
- **Implementation:** Nextcloud MCP (cbcoutinho/nextcloud-mcp-server)
- **Status:** planned
- **Notes:** 90+ tools for Notes, Calendar, Contacts, Files, Deck

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
| 2026-01-30 | node-pairing | skippy | success | Windows + Linux nodes connected |
| 2026-01-30 | cron-fix | skippy | success | Fixed broken cron (sessionTarget gotcha) |
| 2026-01-30 | proxmox-scripting | skippy | success | VM setup scripts for OVH |
| 2026-01-30 | infrastructure-research | skippy | success | Proxmox vs bare metal decision |

---

## Patterns Worth Documenting

### Script Generation Pattern
When generating bash scripts for infrastructure:
1. Check environment first (storage names, paths, versions)
2. Use `--continue` for wget (resume interrupted downloads)
3. Add existence checks (`qm status`, `[ -f file ]`)
4. Print clear instructions at the end
5. Version numbers in URLs go stale — verify before hardcoding

### Cron Job Pattern  
For cron jobs that need to actually DO something:
- Use `sessionTarget: "isolated"` (not "main")
- Use `agentTurn` (not "systemEvent")
- If run time is <1s, something is wrong
- Test with `moltbot cron trigger <jobId>`

### Memory Pattern
- Daily files: raw notes, capture everything
- MEMORY.md: curated, distilled, maintained
- Auto-recall adds noise — quality memories outrank noisy ones

---

*Add entries as we learn. This is our collective memory of what actually works.*
