# Requirements

What our resources expect from your server. Each product page lists its own
exact requirements — this is the common baseline.

## Framework

**ESX Legacy.** Our current resources target ESX and do not support QBCore.

Check your version:

```
version es_extended
```

Some features need a minimum ESX version. `srp_scoreboard` uses duty-based
counting on **ESX 1.11.0 or newer**; on older builds it counts everyone holding
the job instead of only those on duty.

## Libraries

| Resource | Needed for | Where |
|---|---|---|
| **ox_lib** | UI and utilities | [overextended.dev](https://overextended.dev/) |
| **oxmysql** | Database access | [overextended.dev](https://overextended.dev/) |
| **ox_inventory** | `srp_backpacks` only | [overextended.dev](https://overextended.dev/) |
| **ox_target** | Optional, `srp_backpacks` | Keybind fallback works without it |

## Database

**MySQL or MariaDB**, reachable through `oxmysql`.

Confirm `mysql_connection_string` is set in `server.cfg`. Keep the credentials
in a separate secrets file rather than in `server.cfg` itself, and never commit
either to a public repository.

## Server build

A reasonably recent **artifacts** build. If you are more than a few months
behind, update before reporting a bug — several issues turn out to be fixed
already.

Latest builds: [runtime.fivem.net/artifacts/fivem](https://runtime.fivem.net/artifacts/fivem/)

## Cfx.re account

Escrow-protected resources are granted to the **Cfx.re account you give at
checkout**, and appear in [Keymaster](https://keymaster.fivem.net/) under that
account. A purchase made on a different account will not appear.
