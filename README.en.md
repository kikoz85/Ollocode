# Ollocode

[🇮🇹 Italiano](README.md) · **🇬🇧 English**

[![Sponsor Ollocode](https://img.shields.io/badge/Sponsor-Ollocode-ea4aaa?logo=githubsponsors&logoColor=white)](https://github.com/sponsors/kikoz85)

**[⬇️ Download the latest version for macOS](https://github.com/kikoz85/Ollocode/releases/latest)**

A macOS IDE with an **agent that writes, runs and verifies code using local models only** (Ollama or Apple MLX). Nothing leaves your Mac: no cloud, no API keys.

Describe what you want to build or fix: the agent reads the project, writes the code, runs tests and programs, reads the errors and keeps fixing until the work is verified. It works on local projects and on remote servers over SSH (for example a LAMP stack).

> The screenshots show the Italian interface; the app is also available in English, German, French and Spanish.

![Ollocode](docs/screenshots/01-home.png)

## Main features

### An agent that checks its own work

The agent does not just suggest code: it writes it to the files, runs it and checks the result. It does not accept that the work is done while tests fail, while the latest change has never been executed, or while items remain open on its task list.

![Agent at work](docs/screenshots/02-agente-al-lavoro.png)

![Verified result](docs/screenshots/03-agente-risultato.png)

### Editor, diff, Git and terminal

Monaco editor with inline completion from a local model, diff against the last commit, Git panel with generated commit messages, built-in terminal.

![Diff and terminal](docs/screenshots/04-diff-e-terminale.png)

### Remote projects over SSH (PHP, MySQL, WordPress)

Open a folder on a Linux server with your SSH key: files, terminal and agent work directly on the server. Here the agent created a PHP API and verified it by starting the development server and calling it with `curl`.

![SSH project with PHP](docs/screenshots/05-progetto-ssh-php.png)

### Adapts to your Mac

Ollocode reads the chip and memory and picks the model, context window and response length measured for that class of Mac. If the recommended model is missing, it offers to download it.

![Recommended models for this Mac](docs/screenshots/06-modelli-per-hardware.png)

### Safety

Agent commands run in a macOS sandbox (writes allowed only in the project, temporary folders and tool caches). On SSH projects, commands that would write outside the project folder are blocked. A restore point is created before every turn that changes files.

![Agent safety](docs/screenshots/07-sicurezza-agente.png)

### Plan mode

You can agree on the work before any file is touched: in **Plan** mode the agent reads the project and proposes the steps without changing anything. Ask for any change (drop a step, change a technical choice) until you are happy with the plan. The plan is saved in the project as **PLAN.md** (PIANO.md in Italian), with the steps as a checklist. Then run it **one step at a time** (▶ on a step or *Run the next step*) or all at once: each step is verified and its box in the plan file is ticked automatically.

![Plan mode](docs/screenshots/09-modalita-piano.png)

### The web, with your permission

When up-to-date information is needed (the latest version of a library or its CDN link, the official documentation, an error it cannot solve) the agent can search the web and read pages. Every access asks **Allow**, **Always allow in this conversation** or **Reject**.

![Web access](docs/screenshots/10-accesso-internet.png)

### System installs and configuration, with your permission

The agent can install software, set up cron jobs and services, create an Apache virtual host, even with `sudo`, on your Mac or on the server. Every system command is shown verbatim and runs only when you press **Run**. If sudo is needed, you type the password in the card: it never reaches the model and is never stored.

![System command](docs/screenshots/11-comando-di-sistema.png)

### More

- **Debug routine**: when the same error comes back after three fixes, the agent must first run a diagnosis (only the failing test, printed values) before it can edit files again.
- **Project notes** (`.ollocode/notes.md`): architecture, commands and decisions stay available to the agent across requests.
- **Sub-agents**: the agent can hand a module over to another agent with a clean context.
- **In-app updates**: when a new version is released on GitHub a notice shows what's new; **Update now** downloads it, verifies its signature, installs it and restarts Ollocode.
- Interface languages: Italian, English, German, French, Spanish.

## Which Mac, which model

Every model was measured with the same benchmark: 14 real projects (Go, Python, Node.js, TypeScript, Rust, full-stack web) to build from scratch or fix, passed only when the automated tests pass. Each figure comes from a single run, with a variance of ±1-2 tasks.

| Mac | Agent model (default) | Benchmark | Notes |
|---|---|---|---|
| 16 GB (e.g. Mac mini M4) | `qwen3.5:9b` | 7/14 | small and medium tasks; 7.3 GB with a 32k context |
| 24 GB | `gpt-oss:20b` | 5-6/14 | very fast (a few minutes per task), less consistent |
| 32 GB and more | `qwen3.8:27b-mlx` | 13/14 + PHP/MySQL 4/4 | the most reliable; slower (~10 tokens/s on M1 Max) |

Inline completion in the editor uses `qwen2.5-coder:1.5b` (1 GB). Models tested as agents and discarded: `qwen2.5-coder:7b` and `:14b` (0/14: unreliable tool use), `qwen3:8b` and `qwen3:14b` (0/5).

## Installation

1. Install [Ollama](https://ollama.com) and start it.
2. Download the DMG from the latest [release](https://github.com/kikoz85/Ollocode/releases/latest), open it and drag **Ollocode** to **Applications**.
3. On first launch macOS blocks the app because it is not signed with an Apple Developer certificate: open **System Settings → Privacy & Security** and click **Open Anyway**. Or, from Terminal:
   ```bash
   xattr -dr com.apple.quarantine /Applications/Ollocode.app
   ```
4. Open a project: Ollocode offers to download the right model for your Mac.

Requirements: Apple Silicon Mac (M1 or later) with at least 16 GB of memory.

## Sponsor Ollocode

Ollocode is free and runs entirely on your Mac. If you find it useful, you can support its development on **[GitHub Sponsors](https://github.com/sponsors/kikoz85)** ❤️. The "Sponsor Ollocode" button is also in the app, under **Settings**.

![Sponsor Ollocode from the settings](docs/screenshots/08-sostieni.png)

## Author

Enrico Fanucchi
