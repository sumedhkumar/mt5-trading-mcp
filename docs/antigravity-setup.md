# MetaTrader MCP × Antigravity — Setup Guide

A step-by-step guide to connect your MetaTrader 5 account with Antigravity IDE so you can trade using natural language.

---

## What You'll Need

- **Windows PC** (MetaTrader 5 only runs on Windows)
- **Python 3.10+** installed — [Download here](https://www.python.org/downloads/)
- **MetaTrader 5** installed — [Download here](https://www.metatrader5.com/en/download)
- **MT5 account** — demo or live (you'll need login, password, and server name)
- **Antigravity IDE** installed

---

## Step 1 — Install the MCP Server

Open a terminal (Command Prompt or PowerShell) and run:

```bash
pip install metatrader-mcp-server
```

After installation, find the exact path of the installed executable:

```bash
where metatrader-mcp-server
```

You'll get something like:

```
C:\Users\YourName\AppData\Local\Programs\Python\Python314\Scripts\metatrader-mcp-server.exe
```

**Copy this path — you'll need it in Step 3.**

---

## Step 2 — Enable Algo Trading in MetaTrader 5

1. Open MetaTrader 5
2. Go to `Tools` → `Options`
3. Click the `Expert Advisors` tab
4. Check ✅ `Allow algorithmic trading`
5. Click `OK`

> **Keep MetaTrader 5 running** — the MCP server connects to the running terminal.

---

## Step 3 — Find Your MT5 Terminal Path

You need the path to `terminal64.exe`. Common locations:

```
C:\Program Files\MetaTrader 5\terminal64.exe
C:\Program Files (x86)\MetaTrader 5\terminal.exe
```

To find it: right-click the MetaTrader 5 shortcut on your desktop → **Open file location** → copy the full path to `terminal64.exe`.

---

## Step 4 — Configure MCP in Antigravity

1. Open **Antigravity IDE**
2. Click the **⋯ (three-dot menu)** in the agent/chat panel
3. Select **Manage MCP Servers**
4. Click **Open MCP Config** (or "View raw config")

This opens the file `mcp_config.json`. Paste this config:

```json
{
  "mcpServers": {
    "metatrader": {
      "command": "PASTE_YOUR_METATRADER_MCP_SERVER_PATH_HERE",
      "args": [
        "--login",     "YOUR_MT5_LOGIN",
        "--password",  "YOUR_MT5_PASSWORD",
        "--server",    "YOUR_MT5_SERVER",
        "--transport", "stdio",
        "--path",      "YOUR_MT5_TERMINAL_PATH"
      ]
    }
  }
}
```

**Replace the placeholders:**

| Placeholder | What to put | Example |
|-------------|-------------|---------|
| `PASTE_YOUR_METATRADER_MCP_SERVER_PATH_HERE` | Path from Step 1 | `C:\\Users\\John\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\metatrader-mcp-server.exe` |
| `YOUR_MT5_LOGIN` | Your MT5 account number | `5050878232` |
| `YOUR_MT5_PASSWORD` | Your MT5 password | `myP@ssw0rd` |
| `YOUR_MT5_SERVER` | Your MT5 broker server | `MetaQuotes-Demo` |
| `YOUR_MT5_TERMINAL_PATH` | Path from Step 3 | `C:\\Program Files\\MetaTrader 5\\terminal64.exe` |

> ⚠️ **Use double backslashes** (`\\`) in all paths. JSON requires this.

### Example (filled in)

```json
{
  "mcpServers": {
    "metatrader": {
      "command": "C:\\Users\\John\\AppData\\Local\\Programs\\Python\\Python311\\Scripts\\metatrader-mcp-server.exe",
      "args": [
        "--login",     "5050878232",
        "--password",  "myP@ssw0rd",
        "--server",    "MetaQuotes-Demo",
        "--transport", "stdio",
        "--path",      "C:\\Program Files\\MetaTrader 5\\terminal64.exe"
      ]
    }
  }
}
```

---

## Step 5 — Save and Test

1. **Save** the `mcp_config.json` file
2. The MCP server should connect automatically (you may need to restart Antigravity)
3. Open a chat and type:

> *"What's my account balance?"*

If everything is set up correctly, you'll see your MT5 account info returned.

---

## What You Can Do

Once connected, just ask in natural language:

- *"Show me my account balance"*
- *"What's the current price of EURUSD?"*
- *"Buy 0.01 lots of GBPUSD"*
- *"Show all my open positions"*
- *"Close all losing positions"*
- *"Show me XAUUSD H1 candles from last week"*

---

## Troubleshooting

| Problem | Fix |
|---------|-----|
| **MCP server won't connect** | Make sure MetaTrader 5 is open and running |
| **"metatrader-mcp-server not found"** | Run `pip install metatrader-mcp-server` again, then `where metatrader-mcp-server` to get the correct path |
| **"Connection failed"** | Double-check your login, password, and server name. Make sure algo trading is enabled in MT5 |
| **Wrong paths in JSON** | Use double backslashes (`\\`), not single (`\`) |
| **Server shows in config but no tools appear** | Restart Antigravity IDE |

---

## Where Is the Config File?

The Antigravity MCP config file lives at:

```
Windows:  C:\Users\<YourName>\.gemini\config\mcp_config.json
macOS:    ~/.gemini/config/mcp_config.json
```

You can also open it anytime via: **Antigravity → ⋯ → Manage MCP Servers → Open MCP Config**
