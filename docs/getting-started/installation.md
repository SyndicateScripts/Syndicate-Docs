# Installation

The same five steps apply to every resource. Most support tickets are one of
these being missed.

## 1. Download from Keymaster

Sign in to [keymaster.fivem.net](https://keymaster.fivem.net/) with the **same
Cfx.re account** you used at checkout and download the resource.

!!! warning "Not showing up?"
    A purchase made on a different Cfx.re account will not appear. Open a
    **License / Access Help** ticket and we will move it.

## 2. Extract into `resources`

Keep the folder name **exactly as supplied**. Renaming it breaks `ensure` lines,
internal references and escrow validation.

```
resources/
  [syndicate]/
    srp_scoreboard/
    srp_backpacks/
```

## 3. Install dependencies first

Install everything on the product's requirements page **before** starting the
resource. A missing dependency produces errors that look like a fault in our
code but are not.

## 4. Load order

In `server.cfg`, `ensure` runs top to bottom. Frameworks and shared libraries
must start **before** our resources:

```cfg
ensure oxmysql
ensure es_extended
ensure ox_lib
ensure ox_inventory      # only if the resource needs it
ensure ox_target         # optional

ensure srp_scoreboard
ensure srp_backpacks
```

!!! danger "The single most common mistake"
    `attempt to index a nil value (global 'ESX')` almost always means the
    framework starts *after* the resource. Move the `ensure` line up.

## 5. Full restart

```
restart srp_scoreboard
```
is not enough for a **new** resource. Stop and start the server properly the
first time.

---

## Database

Resources that store data create their tables **automatically on first start**
where possible. Where a `.sql` file is supplied, import it before the first
start or every query will error.

Check the console on first boot: a resource that could not reach the database
says so immediately.

## Configuration

Config files are left **open after escrow**. Edit `config.lua` and the locale
files freely — they are yours. Do not edit files marked as escrow-protected;
they cannot be modified and attempting it breaks the resource.

After changing a config:

```
restart srp_scoreboard
```

## Verifying it worked

1. No red errors in the server console at startup
2. The resource appears in `refresh` / `ensure` output as started
3. The feature works in game

If any of those fail, take the **full** console output to
[Troubleshooting](troubleshooting.md) or a support ticket.
