# srp_scoreboard

A clean, server-authoritative scoreboard for ESX — department counts, a
searchable player list, detailed profile panels and a player reputation system
that persists to your database.

**Free.** [Get it from the store](https://syndicaterp-shop.tebex.io/package/7657747){ .md-button .md-button--primary }

---

## Requirements

| | |
|---|---|
| Framework | **ESX Legacy** |
| Required | `es_extended`, `ox_lib`, `oxmysql` |
| Note | Duty-based counting needs **ESX 1.11.0+**. On older builds everyone holding the job is counted instead. |

See [Requirements](../getting-started/requirements.md) for the general baseline.

## Installation

1. Download from [Keymaster](https://keymaster.fivem.net/)
2. Extract into `resources`, keeping the folder name `srp_scoreboard`
3. Import the supplied **SQL file**
4. Add to `server.cfg`, below the framework:

```cfg
ensure oxmysql
ensure es_extended
ensure ox_lib

ensure srp_scoreboard
```

5. Restart the server fully

Full detail: [Installation](../getting-started/installation.md).

---

## Features

### Departments

Define any number of department cards from ESX jobs. Each card can group several
job names together — `police` + `sheriff`, or `ambulance` + `ems` + `doctor` —
and can count either everyone holding the job, or only players currently **on
duty**.

Counts are tracked in memory from ESX's own server events, so **a client cannot
forge them**.

### Player list

Every row shows name, server ID, Discord username, job badge and reputation.

- Live search across name, ID and job
- Four sort modes: ID, name, reputation, job
- Pagination
- The viewer's own row is **pinned above the list**, so it never moves as the
  roster changes

### Player detail panel

Click any row to expand it:

- Discord avatar, username and ID, pulled from the real Discord Bot API
- Job and rank
- Total playtime and current session length
- Connection time, ping, health and armor

### Admin visibility

Licence identifier and IP address are shown to admins only — and they are
**never sent to anyone else in the first place**, rather than being hidden in
the client where they could be read anyway.

Job information can be restricted the same way.

Admin access works through either:

- an **ACE permission**, or
- your existing **ESX admin group**

whichever you already use. The second needs no `server.cfg` change.

### Reputation

Players rate each other good or bad. Fully server-authoritative:

- Configurable cooldown per rating pair
- Same-IP guard against alt-account self-rating
- Capped history log of who rated whom and when
- Computed trust percentage
- An **export** lets your other resources read any player's reputation

---

## Configuration

The config file stays **open after escrow**. Everything a server owner normally
changes lives there:

- Departments, job names, badges and icons
- The full **colour palette** — recolour the entire panel from the config, with
  no CSS editing
- **Custom icons** — paste any stroke SVG from Lucide, Feather or Tabler
- Panel side, width and screen offsets
- **Every line of visible text**, so translating to any language is one file
- Admin access, Discord settings and all reputation rules

Restart the resource after editing:

```
restart srp_scoreboard
```

---

## Performance

- The refresh loop only runs **while a player actually has the panel open**
- It never touches the database — reputation is cached in memory and updated in
  place
- Discord lookups are lazy, cached, rate-limit aware, and warmed in the
  background on join, so the list never waits on Discord's API

---

## What you receive

- Full config with every option documented inline
- English README covering installation, configuration, the export and
  troubleshooting
- The SQL install file

Config, SQL and readme are open source. The rest is escrow-protected.

---

## Troubleshooting

**Departments show 0 with players online**
: Job names in the config must match your ESX job names exactly, including case.
  If you use duty-based counting, confirm your ESX is 1.11.0 or newer.

**Discord names or avatars missing**
: Check the Discord settings in the config. Lookups are cached, so give it a
  moment after a restart before concluding it is broken.

**Admin fields not visible to an admin**
: Confirm the ACE permission or ESX group in the config matches what that
  account actually holds.

Anything else: [Troubleshooting](../getting-started/troubleshooting.md), or open
a **Script Support** ticket with the full console error.
