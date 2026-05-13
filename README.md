# 🔐 Kali MCP Server × PortSwigger Web Security Labs

> **AI-Assisted Penetration Testing** — Using Model Context Protocol (MCP) to solve 
> real-world web vulnerabilities on PortSwigger Web Security Academy  
> **Stack:** Kali Linux · mcp-kali-server · Claude AI (VS Code) · PortSwigger Labs

---

## 📌 What is kali-mcp-server?

`mcp-kali-server` is an official Kali Linux package that acts as an **API bridge** between 
AI assistants (like Claude) and Kali Linux security tools. Using the **Model Context Protocol (MCP)**, 
it exposes tools like `nmap`, `sqlmap`, `nikto`, `hydra`, and more as callable functions — 
enabling fully **agentic, AI-driven penetration testing workflows**.

### Tools Available via MCP
| Tool | Description |
|---|---|
| `nmap_scan` | Execute Nmap security scanner |
| `sqlmap_scan` | Execute SQLmap SQL injection scanner |
| `nikto_scan` | Execute Nikto web server scanner |
| `gobuster_scan` | Execute Gobuster directory/DNS/vhost scanner |
| `dirb_scan` | Execute Dirb web content scanner |
| `enum4linux_scan` | Execute Enum4linux Windows/Samba enumeration |
| `wpscan_analyze` | Execute WPScan WordPress vulnerability scanner |
| `hydra_attack` | Execute Hydra password cracking tool |
| `john_crack` | Execute John the Ripper password cracker |
| `metasploit_run` | Execute a Metasploit module |
| `execute_command` | Execute an arbitrary command on Kali server |
| `server_health` | Check health status of the Kali API server |

---

## ⚙️ Installation

### Step 1 — Install mcp-kali-server via APT

`mcp-kali-server` is natively available in Kali Linux repositories — no manual build needed.

```bash
sudo apt install mcp-kali-server
```

> ✅ If already installed, APT confirms the latest version is present.

---

### Step 2 — Verify Installation & Start the API Server

First, check available options:
```bash
mcp-server -h
```

Then start the Kali API server (Flask-based, runs on `127.0.0.1:5000`):
```bash
kali-server-mcp
```
> The server starts a Flask app and listens on `http://127.0.0.1:5000`

---

## 🔧 Configuration (VS Code + Claude)

### Step 3 — Create MCP Config Folder and File

Navigate to your project directory and create the MCP config:

```bash
mkdir ~/kali-mcp
cd ~/kali-mcp
nano .vscode/mcp.json
```
Paste this configuration:

```json
{
  "servers": {
    "mcp-kali": {
      "command": "mcp-server",
        "args": [
          "--server",
          "http://127.0.0.1:5000/"
        ],
        "description": "MCP Kali Server",
        "timeout": 3000,
        "alwaysAllow": []
    }
  }
}
```

---

### Step 4 — Alternative Config Format (Servers key)

Some versions of the VS Code MCP extension use a `Servers` key instead:

```json
{
  "mcpServers": {
    "mcp-kali-server": {
      "command": "python3",
        "args": [
          "/absolute/path/to/client.py",
          "--server",
          "http://LINUX_IP:5000/"
        ],
        "description": "MCP Kali Server",
        "timeout": 300,
        "alwaysAllow": []
    }
  }
}
```

---

### Step 5 — Open Project in VS Code

```bash
code .
```
---

### Step 6 — Verify MCP Server is Detected

In VS Code: `Ctrl+Shift+P` → **Agent Customizations** → **MCP Servers**

You should see `mcp-kali` listed (may show as "Stopped" initially).

![MCP Server Setup](screenshots/Screenshot%202026-05-12%20112712.png)

---

### Step 7 — Start the MCP Server from VS Code

Right-click `mcp-kali` → **Start Server**

![Start Server](screenshots/Screenshot%202026-05-12%20112753.png)

Once connected, the Output panel confirms **12 tools discovered** and shows:
```
[INFO] Successfully connected to Kali API server at http://127.0.0.1:5000/
[INFO] Server health status: healthy
[INFO] Discovered 12 tools
```
![Kali MCP Logs](screenshots/Screenshot%202026-05-12%20153604.png)

---

## 🧪 Lab Walkthrough

### Lab01: SQL Injection Vulnerability Discovery
**Platform:** PortSwigger Web Security Academy  
**Category:** SQL Injection  
**Difficulty:** Apprentice/Practitioner

#### Prompt Given to Claude (via MCP)

```
find the sql injection bug on this server
https://0a25004b04705b8b80d244f600730080.web-security-academy.net/
using mcp-kali and professional report of this bug
```

#### How Claude Used the MCP Tools
1. Claude called `mcp-kali` via MCP on the target URL
2. Identified injectable parameters automatically
3. Generated a professional vulnerability report

---


### Lab02: Path Traversal Vulnerability Discovery
**Platform:** PortSwigger Web Security Academy  
**Category:** Path Traversal  
**Difficulty:** Apprentice/Practitioner

#### Prompt Given to Claude (via MCP)

```
find the sql injection bug on this server
https://0a5d00d103b873d48035e444007800e5.web-security-academy.net/
using mcp-kali and professional report of this bug
```

#### How Claude Used the MCP Tools
1. Claude called `mcp-kali` via MCP on the target URL
2. Identified injectable parameters automatically
3. Generated a professional vulnerability report
---
