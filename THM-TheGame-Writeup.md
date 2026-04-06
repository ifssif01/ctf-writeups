# TryHackMe — The Game | CTF Write-up

**Platform:** TryHackMe  
**Room:** The Game  
**Difficulty:** Easy  
**Category:** Reverse Engineering / Static Analysis  
**Flag:** `THM{I_CAN_READ_IT_ALL}`

---

## Overview

The challenge provides a zip file containing `Tetrix.exe` — a Tetris-like game built with the Godot engine. The goal is to find the hidden flag without necessarily running the executable.

---

## Approach

Since the flag is embedded as a plaintext string inside the binary, there's no need to execute the `.exe` or decompile the Godot project. The `strings` utility extracts all printable ASCII sequences from a binary, making it the fastest path to the flag.

---

## Solution

### Step 1 — Extract strings from the binary

```bash
strings Tetrix.exe | grep -iE "THM\{"
```

### Output

```
THM{I_CAN_READ_IT_ALL}
```

That's the flag.

---

## Key Takeaway

Before reaching for heavier tools (decompilers, sandboxes, dynamic analysis), always run `strings` on an unknown binary. Developers often leave plaintext secrets — flags, credentials, keys — embedded directly in executables. It takes seconds and costs nothing.

This approach also works natively on macOS and Linux with no extra tools required.

---

## Tools Used

| Tool | Purpose |
|------|---------|
| `strings` (built-in) | Extract printable ASCII from binary |
| `grep` (built-in) | Filter output for the flag format |
