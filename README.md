# Don't Starve Together Mod Loading Issue – Workaround

## Problem Description

Fix *Don't Starve Together* (DST) Workshop mods not loading after moving game installation via Steam.
In a local Steam installation of DST, a set of 19 subscribed mods failed to load correctly in the in‑game Mods interface.

Observed symptoms:

* Some mods did not render at all in the Mods list.
* Some mods appeared as incompatible or placeholder entries.
* The number and identity of incompatible mods changed after restarting the game or modifying subscriptions.
* In `steamapps/Workshop/Content/322330`, certain mod directories existed but contained no actual mod data (only legacy or empty files).
* Re-subscribing affected mods via Steam did not consistently restore valid mod content.

This indicated a desynchronization between:

* Steam Workshop subscription state
* Workshop cache (`Workshop/Content/322330`)
* Local mod loading logic in `Don't Starve Together/mods`

Directly relying on Steam subscription alone was insufficient to restore a consistent, fully loaded mod set.

## Workaround

The following manual process resulted in a stable state where all 19 mods were successfully loaded in-game.

### Environment

* Steam library located on drive `D:`
* Paths used:

  * Workshop cache: `D:\games\steamapps\Workshop\Content\322330`
  * Local mods directory: `D:\games\steamapps\common\Don't Starve Together\mods`

### Steps

1. **Backup existing Workshop mods**

   * Copy all 19 mod folders from `Workshop\Content\322330`.
   * Add the prefix `workshop_` to each folder name.
   * Store them in a temporary backup directory (e.g. `tmp`).

2. **Prevent immediate cleanup by DST**

   * Set the `mods` directory properties to *read-only*.
   * Launch DST once.
   * Result:

     * DST reset directory permissions.
     * The `workshop_xxx` folders were preserved.
     * The Mods UI began showing previously missing/incompatible entries, confirming partial recognition.

3. **Reset Steam subscription state**

   * Unsubscribe from *all* DST mods in Steam.
   * Launch DST.
   * Result:

     * 14 mods appeared as loaded.
     * 5 mods appeared as incompatible placeholders.

4. **Identify corrupted mods**

   * Inspect the 5 incompatible mods in `Workshop\Content\322330`.
   * Observation:

     * Their directories contained no valid mod data (empty or legacy-only).

5. **Recover corrupted mods**

   * Delete the 14 valid mods from the local mods directory (they were already backed up).
   * Re-subscribe only to the 5 corrupted mods in Steam.
   * Launch DST.
   * Result:

     * The 5 mods were freshly downloaded.
     * Valid data appeared in `Workshop\Content\322330`.

6. **Reconstruct full mod set manually**

   * Copy the newly downloaded 5 mods.
   * Add `workshop_` prefix and back them up.
   * Combine:

     * 14 previously backed-up mods
     * 5 freshly recovered mods
   * Place all 19 `workshop_xxx` folders into `Don't Starve Together\mods`.

7. **Final state**

   * Launch DST.
   * All 19 mods load correctly and appear normally in the Mods interface.
   * Steam subscription status:

     * 5 mods subscribed (update-capable)
     * 14 mods manually installed (static, no auto-update)

### Notes and Limitations

* This is a **stable but temporary** equilibrium.
* Manually installed mods will **not receive Steam updates**.
* Updating those mods requires repeating parts of this process.
* The issue appears related to partial or failed Workshop downloads combined with DST’s mod cache behavior.

---

This document records the workaround as a reproducible recovery procedure rather than a permanent fix.
