# srp_backpacks

Unique, persistent backpacks for ESX Legacy and ox_inventory.

Every backpack is an individual piece of property. Two identical items are never
interchangeable: each one carries its own identity, its own storage and its own
contents. Hand one to another player, sell it, throw it in a car boot or drop it
in a field — the contents travel with **that specific piece** and nothing else.

**€4.99.** [Get it from the store](https://syndicaterp-shop.tebex.io/package/7658432){ .md-button .md-button--primary }

---

## Requirements

| | |
|---|---|
| Framework | **ESX Legacy** — QBCore is not supported |
| Required | `ox_lib`, `ox_inventory`, `oxmysql` |
| Database | MySQL or MariaDB |
| Optional | `ox_target` — a keybind fallback works without it |

See [Requirements](../getting-started/requirements.md) for the general baseline.

## Installation

1. Download from [Keymaster](https://keymaster.fivem.net/)
2. Extract into `resources`, keeping the folder name `srp_backpacks`
3. Paste the supplied **item definitions and images** into `ox_inventory`
4. Add to `server.cfg`, below the framework and inventory:

```cfg
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure ox_inventory
ensure ox_target        # optional

ensure srp_backpacks
```

5. Restart the server fully

!!! success "No manual SQL"
    Database tables are created **automatically on first start**.

Full detail: [Installation](../getting-started/installation.md).

---

## Features

### Wear it, drop it, pick it back up

- Backpacks show on the character using the **clothing component**, with
  separate male and female values per type
- A watchdog restores the visual after clothing shops or outfit changes wipe it
- Drop a backpack in the world and **open it where it lies**
- Picking it up puts it straight back on your shoulders, not into your pockets
- Dropped backpacks are stored in the database and return to the **exact same
  spot** after a server restart
- `ox_target` support, with an ++e++ / ++g++ keybind fallback when `ox_target`
  is not installed

### Built server-side

The client asks; the server decides. Ownership, distance, capacity, item
restrictions and player state are validated server-side on every action, and
again inside the `ox_inventory` hooks that every item move has to pass through.

- A backpack exists in exactly **one place at a time**: an inventory item, a
  worn record, or a ground record
- A **unique database index** makes it physically impossible for two players to
  wear the same piece
- Capacity is read from the config by type, **never from item metadata** — so
  forged metadata cannot grant a bigger backpack
- Backpacks inside backpacks are blocked, and a backpack can never be put inside
  itself
- Suspicious attempts are logged with the player's licence and Discord ID

---

## Configuration

Everything below is editable without touching protected code:

- **Four backpack types included**; add as many as you like from a single config
  file
- Per type: slots, weight, price, prop model, clothing values, blacklists and
  whitelists
- Per-type carry limits, weapon and item restrictions, dynamic weight
- **English and Czech included**, language selected in the config — add your own
  by copying one JSON file
- **Appearance bridge** for `illenium-appearance`, `fivem-appearance`,
  `esx_skin` / `skinchanger` and native calls, in an open file you can edit
- Admin tools for repairing, restoring, inspecting and destroying backpacks
- Optional **Discord webhook logging** per event type
- In-game helper commands for finding clothing values and prop models

Restart the resource after editing:

```
restart srp_backpacks
```

---

## What you receive

- The escrow-protected resource, ready to drop into your server
- `config.lua`, the backpack definitions, the appearance bridge and all locale
  files left **open** for you to edit
- Item definitions and images ready to paste into `ox_inventory`
- Database tables created automatically on first start
- Full documentation: installation, configuration, API, FAQ and troubleshooting

## How you receive it

You are asked for your **Cfx.re account name at checkout**. The asset is granted
to that account and appears in your
[Keymaster](https://keymaster.fivem.net/), where you can download and
re-download it any time. Updates are delivered through Keymaster as well.

---

## Troubleshooting

**The backpack does not appear on the character**
: Clothing values in the config must match your clothing pack, and are separate
  for male and female. Use the included in-game helper command to find the right
  values. If it appears and then vanishes, an appearance resource is overwriting
  it — check the appearance bridge is set to the one you actually run.

**Items vanish when moving a backpack**
: This should be impossible; every move passes through the `ox_inventory` hooks.
  Open a **Bug Report** ticket with the console output and the exact steps.

**"You cannot put a backpack inside a backpack"**
: Working as intended. Nesting is blocked deliberately, because it makes
  capacity limits meaningless.

**A dropped backpack disappeared after a restart**
: Dropped backpacks persist in the database. If one did not return, check
  `oxmysql` connected successfully at startup — nothing persists if the database
  was unreachable.

**ox_target does not show the option**
: The keybind fallback works without `ox_target`. If it is installed but not
  offering the option, confirm it started **before** `srp_backpacks`.

Anything else: [Troubleshooting](../getting-started/troubleshooting.md), or open
a **Script Support** ticket with the full console error.

---

## Support scope

Support covers **installation, configuration and defects**.

It does not cover conflicts with third-party resources, custom feature
development, or modified core resources.
