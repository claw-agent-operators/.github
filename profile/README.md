## Tools for claw agent operators

Running claw agents in production means dealing with a fragmented ecosystem:
multiple architectures, incompatible CLIs, no standard way to migrate or manage
across installations. These tools fill that gap.

---

### [claw](https://github.com/claw-agent-operators/claw)
<a href="https://github.com/claw-agent-operators/claw">
<p align="left">
  <img src="https://raw.githubusercontent.com/claw-agent-operators/claw/refs/heads/main/assets/terminal-grip.svg" alt="Claw" width="100" />
</p>
</a>

Universal CLI for claw agent architectures. One binary to run agents, watch
conversations, and inspect running instances — across NanoClaw, ZeptoClaw,
OpenClaw, PicoClaw, and others.
```
claw agent "What is 2+2?"
claw ps
claw watch -g main
claw health
claw api serve --console
```
Ships with NanoClaw and ZeptoClaw drivers. Uses architecture-specific driver
binaries via NDJSON on stdin/stdout — no plugins, no shared libraries, no
version coupling.

---

### [molt](https://github.com/claw-agent-operators/molt)
<a href="https://github.com/claw-agent-operators/molt">
<p align="left">
  <img src="https://raw.githubusercontent.com/claw-agent-operators/molt/refs/heads/main/assets/double-shell.svg" alt="Molt" width="100">
</p>
</a>

Move your agents between architectures. Exports groups, memory, skills,
conversations, and scheduled tasks into a portable `.molt` bundle, then imports
into any supported target.

```
molt export ~/nanoclaw-install --out my-agents.molt
molt export ~/nanoclaw-install --include surf-crew
molt import my-agents.molt ~/new-install --arch zepto
molt sync init ~/nanoclaw-install
molt restore
```
Ships with NanoClaw and ZeptoClaw drivers. Also available via `claw molt`.

---

### [claw-console](https://github.com/claw-agent-operators/claw-console)

Web dashboard for `claw api serve`. Vite + React + TypeScript SPA with
shadcn/ui. No backend of its own — connects directly to the claw API.

Health tiles, running agents, live message feed, browser REPL, session history,
group config. Embedded in the claw binary via `claw api serve --console` or
hosted standalone.

---

### Driver protocol

Both tools use the same driver discovery pattern: install a
`claw-driver-<arch>` or `molt-driver-<arch>` binary anywhere in
`~/.claw/drivers/` or `$PATH`. Drivers are standalone executables speaking
NDJSON — any language works. See the driver spec in each repo.
