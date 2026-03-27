## Tools for claw agent operators

Running claw agents in production means dealing with a fragmented ecosystem:
multiple architectures, incompatible CLIs, no standard way to migrate or manage
across installations. These tools fill that gap.

---

### [claw](https://github.com/claw-agent-operators/claw)

Universal CLI for claw agent architectures. One binary to run agents, watch
conversations, and inspect running instances — across NanoClaw, ZeptoClaw,
OpenClaw, PicoClaw, and others.
claw repl -g main
claw ps
claw watch -g dev
Uses architecture-specific driver binaries via NDJSON on stdin/stdout.
No plugins, no shared libraries, no version coupling.

---

### [molt](https://github.com/claw-agent-operators/molt)

Move your agents between architectures. Exports groups, memory, skills,
conversations, and scheduled tasks into a portable `.molt` bundle, then imports
into any supported target.
molt export ~/nanoclaw-install --out my-agents.molt
molt import my-agents.molt ~/new-install --arch zepto
---

### Driver protocol

Both tools use the same driver discovery pattern: install a
`claw-driver-<arch>` or `molt-driver-<arch>` binary anywhere in
`~/.claw/drivers/` or `$PATH`. Drivers are standalone executables speaking
NDJSON — any language works. See the driver spec in each repo.
