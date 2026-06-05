# MT5Client Sub-module 🤖

Welcome to the **MT5Client** documentation! This is your all-in-one Python interface for MetaTrader 5 automation: connect, trade, analyze, and manage your MT5 terminal with a single, unified client. Perfect for algo trading, analytics, and robust trading automation! 🚀

---

## Purpose 🎯

The `MT5Client` class is the main entry point for all MetaTrader 5 operations in this library. It wraps and unifies connection, account, market, order, and history management into a single, easy-to-use object.

---

## Class Overview 🏗️

```python
from metatrader_client.client import MT5Client
```

- **Class:** `MT5Client`
- **Location:** `src/metatrader_client/client.py`
- **Submodules:**
  - `.account` → Account info and status
  - `.market` → Market data and symbol info
  - `.order` → Trading and order management
  - `.history` → Historical deals and orders
  - `.connection` → Terminal connection management

---

## Initialization ⚙️

```python
from metatrader_client.client import MT5Client

# Minimal configuration
config = {
    "login": 12345678,
    "password": "your_password",
    "server": "Broker-Server"
}

# Full configuration with all available options
config = {
    "login": 12345678,           # Required: MT5 account login number
    "password": "your_password",  # Required: MT5 account password
    "server": "Broker-Server",    # Required: MT5 server name
    "path": None,                 # Optional: Path to terminal executable (auto-detect if None)
    "timeout": 60000,             # Optional: Connection timeout in ms (default: 60000)
    "portable": False,            # Optional: Use portable mode (default: False)
    "max_retries": 3,             # Optional: Max connection retries (default: 3)
    "backoff_factor": 1.5,        # Optional: Retry delay multiplier (default: 1.5)
    "cooldown_time": 2.0,         # Optional: Seconds between connections (default: 2.0)
    "debug": False                # Optional: Enable debug logging (default: False)
}

client = MT5Client(config)
```

### Configuration Parameters

| Parameter | Type | Required | Default | Description |
|-----------|------|----------|---------|-------------|
| `login` | int | Yes | - | Your MT5 account login number |
| `password` | str | Yes | - | Your MT5 account password |
| `server` | str | Yes | - | MT5 server name (e.g., "MetaQuotes-Demo") |
| `path` | str | No | None | Full path to MT5 terminal executable (auto-detected if not provided) |
| `timeout` | int | No | 60000 | Connection timeout in milliseconds |
| `portable` | bool | No | False | Enable portable mode for MT5 terminal |
| `max_retries` | int | No | 3 | Maximum number of connection retry attempts |
| `backoff_factor` | float | No | 1.5 | Exponential backoff factor for retry delays |
| `cooldown_time` | float | No | 2.0 | Minimum time in seconds between connection attempts |
| `debug` | bool | No | False | Enable detailed debug logging for troubleshooting |

---

## Main Attributes & Methods 🧩

### Attributes (Submodules)
- `client.account` — Account operations (balance, equity, margin, etc.)
- `client.market` — Market data (symbols, prices, candles)
- `client.order` — Order management (positions, orders, trading)
- `client.history` — Historical deals/orders/statistics

### Connection Methods
- `connect()` — Connect to the MT5 terminal and login
- `disconnect()` — Disconnect from the terminal
- `is_connected()` — Check connection status
- `get_terminal_info()` — Get terminal details
- `get_version()` — Get terminal version
- `last_error()` — Get last error code/description

---

## Example Usage 💡

```python
from metatrader_client.client import MT5Client

config = {
    "login": 12345678,
    "password": "your_password",
    "server": "Broker-Server"
}

client = MT5Client(config)
if client.connect():
    print("Connected! 🎉")
    print("Balance:", client.account.get_balance())
    print("EURUSD price:", client.market.get_symbol_price("EURUSD"))
    client.order.place_market_order(type="buy", symbol="EURUSD", volume=0.1)
    print("Recent deals:", client.history.get_deals())
    client.disconnect()
else:
    print("Failed to connect. 🚨")
```

---

## Submodule Docs 📚
- [Connection](./_connection.md)
- [Account](./_account.md)
- [Market](./_market.md)
- [Order](./_order.md)
- [History](./_history.md)

---

## Tips & Troubleshooting 🛡️
- Ensure the [MetaTrader5 Python package](https://pypi.org/project/MetaTrader5/) is installed.
- Use the `debug` flag in your config for more logs.
- Handle exceptions for robust automation.
- See submodule docs above for detailed info.

---

## Happy Trading! 📈🤖

For more details, see the source code in `src/metatrader_client/client.py` and the submodules.
