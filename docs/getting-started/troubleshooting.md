# Troubleshooting

Common console errors and what they actually mean.

!!! tip "Read the first error, not the last"
    The **first** error in the console is usually the cause. Everything after it
    is often a consequence. Scroll up.

---

## `attempt to index a nil value (global 'ESX')`

The framework object was never obtained. Almost always **load order**:
`es_extended` starts after the resource that needs it.

**Fix:** move `ensure es_extended` above our resources in `server.cfg`, then
restart the server fully.

Other causes:

- The resource expects ESX but the server runs QBCore
- A very old or heavily modified ESX with a renamed export

---

## `Failed to load script: @resource/file.lua`

The file is missing, or it has a syntax error.

- Check the folder name was not renamed
- Check `fxmanifest.lua` lists the file
- **Capitalisation matters on Linux** and not on Windows, so a resource can
  work locally and fail in production

---

## `attempt to call a nil value (field 'xxx')`

A function does not exist on the object being called — normally a **version
mismatch**. The resource expects a newer or older version of a dependency than
the one installed.

Check `ox_lib`, `ox_inventory` and `es_extended` are current.

---

## `oxmysql was unable to connect` / `ER_ACCESS_DENIED`

Database connection failure. Check `mysql_connection_string` in `server.cfg`:
host, port, user, password and database name.

Nothing that touches the database will work until this is resolved.

---

## `No such export xxx in resource yyy`

The resource providing the export is not started, started too late, or is a
version without that export.

---

## `[ERROR] Resource "xxx" is not allowed to load`

An **escrow** error. The resource is not authorised for the server key it is
running under.

1. Open [Keymaster](https://keymaster.fivem.net/)
2. Check the resource is assigned to the **server key this server actually uses**
3. If it is assigned correctly and still fails, open a **License / Access Help**
   ticket

---

## `Couldn't start resource xxx`

The resource failed during load. The real error is usually a few lines **above**
this one.

---

## It starts, but nothing happens in game

- Confirm the resource is actually running: `ensure` output, or `refresh` then
  `start`
- Check your `config.lua` — a feature may be disabled by default
- Check you meet the in-game condition: correct job, on duty, correct item

---

## Isolating a conflict

If the error is not obvious, test with **only** the framework, the dependencies
and our resource loaded.

- Problem gone → another resource is conflicting. Add resources back in halves
  until it returns; that names the culprit in a few restarts.
- Problem remains → it is ours. Open a ticket with the full console output.

Knowing which resource conflicts is the fastest route to a fix, and it is
something only you can test on your own server.

---

## Before opening a ticket

Have these ready. A ticket without them takes several messages before anyone
can even start:

- Product name and **version**
- Framework and **artifacts** version
- The **complete** console error, as text, not a screenshot of one line
- Steps to reproduce
- What you expected versus what happened
- Whether it still happens on a clean server

!!! warning "Never post publicly"
    Licence keys, server keys, database credentials or your Tebex transaction
    ID. Staff will never ask for your password or payment details.
