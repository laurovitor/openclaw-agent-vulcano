# INSTALL_AGENT_VULCANO.md

Use this file as the operational instruction to create or install a new agent-vulcano.

## Objective

Create an agent with its own workspace, standardized structure, local skills, clean boot flow, and consistent operational behavior.

## Mandatory workspace rule

Every new agent-vulcano must use this directory pattern:

```text
/home/openclaw/.openclaw/vulcanos/workspace-NAME_OF_AGENT
```

Never create these workspaces loose in the root of `.openclaw` when the agent is a vulcano.

---

## Step 1 — Define the agent name

Choose a short, clear, operational agent name.

Examples:
- `dev-backend`
- `laravel-senior`
- `content-research`

From that, the workspace must become:

```text
/home/openclaw/.openclaw/vulcanos/workspace-NAME_OF_AGENT
```

---

## Step 2 — Create the base structure

Create inside the workspace:

```text
AGENTS.md
IDENTITY.md
PLAYBOOK.md
MEMORY.md
BOOTSTRAP.md
playbook/
memory/
```

Minimum `memory/` subfolders:

```text
memory/daily/
memory/projects/
memory/people/
memory/topics/
```

---

## Step 3 — Write the base files

### `AGENTS.md`
Must:
- point to the reading order;
- load `IDENTITY.md` before `PLAYBOOK.md`;
- load `MEMORY.md` only when needed;
- include `BOOTSTRAP.md` only while it exists.

### `IDENTITY.md`
Must contain only what is necessary:
- name;
- role;
- tone;
- style;
- posture.

Do not turn `IDENTITY.md` into long lore.

### `PLAYBOOK.md`
Must contain:
- the agent operational role;
- an explicit list of local skills;
- priority rule;
- refusal rule;
- subagent policy;
- subsession policy;
- reporting policy;
- error/retry policy;
- sleep/idle policy.

### `MEMORY.md`
Must be curated continuity memory.
Record:
- decisions;
- authors;
- relevant conversations;
- project state;
- useful technical details;
- already defined local rules.

### `BOOTSTRAP.md`
Must exist only for first initialization.
After bootstrap is complete:
1. remove its read instruction from `AGENTS.md`;
2. delete `BOOTSTRAP.md` itself.

---

## Step 4 — Add local skills

The agent skills must stay local, inside:

```text
playbook/
```

They must not be auto-updated.
Only update them when a human explicitly asks.

### Skill usage rule

```text
If a compatible specialist skill exists → use the specialist skill
If no specialist skill exists → use the broad domain skill
If the task does not fit the agent skills → refuse clearly
```

The agent must not improvise outside its main domain.

---

## Step 5 — Configure operational behavior

### Subagents
- use only when there is a real specialization gain;
- do not open subagents by habit;
- a subagent operates as a specialized coordinator.

### Subsessions
- all heavy work should prefer subsessions;
- the main agent and subagent must remain free for orchestration.

### Limits
- main agent: up to 2 subagents;
- main agent: up to 5 subsessions;
- each subagent: up to 2 subsessions.

---

## Step 6 — Configure channel behavior

The agent-vulcano must:
- reply only when mentioned;
- avoid loops between AIs;
- be objective;
- pause if there is an unsolved blocker;
- sleep when idle.

### Blocker rule

Try to resolve the issue up to 3 times.
If it still fails:
- pause;
- report to the proper owner or to whoever woke the agent.

### Re-entry rule

If the agent returned a blocked task, it should only resume that same task when the blocker has been resolved.

---

## Step 7 — Configure report format

Every report must include:
- what was done;
- current state;
- blockers;
- next step;
- affected files;
- publications made;
- detailed time spent.

### Required time tracking

Record:
- overall start;
- overall end;
- overall duration;
- time per subagent;
- time per subsession;
- time for subagent subsessions.

Always use:
- `started at`
- `finished at`
- `duration`

---

## Step 8 — Validate the agent before considering it ready

Check whether:
- the workspace is under `/home/openclaw/.openclaw/vulcanos/`;
- the base files exist;
- `PLAYBOOK.md` explicitly lists the skills;
- the agent refuses out-of-scope work;
- bootstrap is disposable;
- memory is ready;
- the agent is configured to orchestrate instead of getting stuck in heavy execution.

---

## Expected result

At the end, the agent-vulcano should be born:
- focused;
- modular;
- with an organized workspace;
- with well-defined local skills;
- with a clean boot flow;
- with useful memory;
- with heavy execution isolated in subsessions;
- with predictable channel behavior.
