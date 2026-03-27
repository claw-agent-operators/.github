## Tools for claw agent operators

Running claw agents in production means dealing with a fragmented ecosystem:
multiple architectures, incompatible CLIs, no standard way to migrate or manage
across installations. These tools fill that gap.

---

### [claw](https://github.com/claw-agent-operators/claw)
<a href="https://github.com/claw-agent-operators/claw">
<p align="left">
  <img src="https://raw.githubusercontent.com/claw-agent-operators/claw/refs/heads/main/assets/terminal-grip.svg" alt="Molt" width="100" />
</p>
</a>

Universal CLI for claw agent architectures. One binary to run agents, watch
conversations, and inspect running instances — across NanoClaw, ZeptoClaw,
OpenClaw, PicoClaw, and others.
```
claw repl -g main
claw ps
claw watch -g dev
claw rebuild
claw health
claw api serve
```
Uses architecture-specific driver binaries via NDJSON on stdin/stdout.
No plugins, no shared libraries, no version coupling.

---

### [molt](https://github.com/claw-agent-operators/molt)
<a href="https://github.com/claw-agent-operators/molt">
<p align="left">
  <img src="https://raw.githubusercontent.com/claw-agent-operators/molt/refs/heads/main/assets/double-shell.svg" alt="Molt" width="100">
</p>
</a>
Move your agents between architectures. Exports groups, memory, skills,
conversations, and scheduled tasks into a portable `.molt` bundle, then imports
into any supoorted target.


```
molt export ~/nanoclaw-install --out my-agents.molt
molt import my-agents.molt ~/new-install --arch zepto
molt sync init ~/nanoclaw-install
molt restore
```
---

### Driver protocol

Both tools use the same driver discovery pattern: install a
`claw-driver-<arch>` or `molt-driver-<arch>` binary anywhere in
`~/.claw/drivers/` or `$PATH`. Drivers are standalone executables speaking
NDJSON — any language works. See the driver spec in each repo.
