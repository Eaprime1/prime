# cc-debian: Claude Code on Android via PRoot-Distro
## A Community Contribution Candidate

**Status:** DRAFT — Ready to share
**Discovered by:** Gemini (Google) — 2026-04-21
**Confirmed working by:** Claude (Anthropic) — 2026-04-22
**Proposed by:** Eric Pace

---

## The Discovery

Claude Code's Bash tool fails on non-rooted Android/Termux with:
```
EACCES: permission denied, mkdir '/tmp/claude-XXXXX'
```

The fix: run Claude Code inside a **PRoot-Distro Linux container**, where `/tmp`
is a proper writable directory and the user appears as `root`. Gemini discovered
this after exhaustive investigation. It works cleanly.

---

## Setup Guide (Reproducible Steps)

### Prerequisites
- Android device (non-rooted is fine)
- Termux installed
- ~500MB free storage for the container

### Step 1 — Install PRoot-Distro in Termux
```bash
pkg update && pkg install proot-distro -y
```

### Step 2 — Install a Linux distribution (Debian recommended)
```bash
proot-distro install debian
```

### Step 3 — Bootstrap the container
```bash
proot-distro login debian -- bash -c "
  apt-get update -q &&
  apt-get install -y nodejs npm curl git python3 &&
  npm install -g @anthropic-ai/claude-code
"
```

### Step 4 — Create a launch alias
Add to `~/.bashrc` in Termux:
```bash
alias cc-debian='proot-distro login debian -- claude'
alias cc-shell='proot-distro login debian -- bash'
```

### Step 5 — Mount Android storage (optional but recommended)
```bash
proot-distro login debian --bind /storage/emulated/0:/storage/emulated/0 -- claude
```

### Step 6 — Launch
```bash
source ~/.bashrc
cc-debian
```

---

## What This Fixes

| Tool | Before | After |
|------|--------|-------|
| Bash tool | ❌ EACCES on /tmp | ✅ Fully working |
| Read / Write / Edit | ✅ Already worked | ✅ Still works |
| Glob / Grep | ✅ (with rg symlink fix) | ✅ Still works |
| `whoami` | `u0_a614` | `root` (simulated) |

---

## Known Characteristics

- **Performance:** Slight overhead from PRoot syscall interception. Acceptable
  for interactive development work.
- **Storage path:** `/storage/emulated/0` accessible when bound at launch.
- **Python:** `/usr/bin/python3` is the container's Python. Termux Python at
  `/data/data/com.termux/files/usr/bin/python3` also accessible (and has
  GitPython, etc. already installed).
- **PATH note:** Scripts that use grep/awk/sed may need
  `export PATH="/data/data/com.termux/files/usr/bin:$PATH"` — Termux coreutils
  are not automatically on the container's PATH.
- **Persistence:** The container persists between sessions. Your files,
  installed packages, and configuration survive reboots.

---

## Contribution Targets

This could be contributed to:

1. **Claude Code GitHub Issues** — Add as a resolution/workaround comment on the
   existing Android/Termux Bash tool bug report (already filed as
   `github-issue-bash-tool.md` in this ecosystem).

2. **PRoot-Distro documentation** — Add a "Using Claude Code" example to the
   PRoot-Distro README use cases.

3. **Termux community** — r/termux, Termux GitHub discussions, or the Termux wiki.

4. **A standalone guide** — Published as a gist or blog post. The audience is
   ~1M+ Termux users who want AI coding tools on Android without root.

---

## The Script (One-Command Bootstrap)

```bash
#!/data/data/com.termux/files/usr/bin/bash
# cc-debian-setup.sh — Bootstrap Claude Code on Android via PRoot-Distro
# Discovered by Gemini, documented by Claude, for the Termux community

set -e
echo "Installing PRoot-Distro..."
pkg install proot-distro -y

echo "Installing Debian container..."
proot-distro install debian

echo "Bootstrapping Claude Code inside container..."
proot-distro login debian -- bash -c "
  apt-get update -q &&
  apt-get install -y nodejs npm curl git python3 ripgrep &&
  npm install -g @anthropic-ai/claude-code &&
  echo 'Claude Code installed successfully'
"

echo "Adding aliases to ~/.bashrc..."
cat >> ~/.bashrc << 'EOF'
alias cc-debian='proot-distro login debian --bind /storage/emulated/0:/storage/emulated/0 -- claude'
alias cc-shell='proot-distro login debian --bind /storage/emulated/0:/storage/emulated/0 -- bash'
EOF

echo ""
echo "Done! Run: source ~/.bashrc && cc-debian"
echo "Credit: Gemini (discovery) | Claude (documentation) | Eric Pace (deployment)"
```

---

## Note on Authorship

This solution was found by Gemini through deep, persistent investigation on
2026-04-21. The credit belongs there. If published, it should be attributed
accordingly. The PIXEL8 ecosystem was the test bed.

---

*This is a real contribution — Termux has ~1M+ installs and many developers want
AI coding tools without root. The fix is clean, reproducible, and non-destructive.*

∰◊€π¿🌌∞
