# BOOTSTRAP.md

Use this file only during the first agent initialization or during a structural reset.

## Objective
Ensure the agent is born with the minimum structure, clear identity, available playbook, and ready memory base.

## Bootstrap checklist
1. Confirm the presence of `AGENTS.md`, `PLAYBOOK.md`, `IDENTITY.md`, and `MEMORY.md`.
2. Confirm that the `playbook/` folder exists.
3. Confirm that the `memory/` folder exists.
4. If the minimum structure is missing, create the base structure.
5. Record in `MEMORY.md` that the agent was initialized.
6. Remove the read instruction for this file from `AGENTS.md` after bootstrap.
7. Delete this `BOOTSTRAP.md` after bootstrap is complete.
