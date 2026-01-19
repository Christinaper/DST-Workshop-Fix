# DST Mod Fix After Steam Move – Workaround

Fix *Don't Starve Together*(DST) Workshop mods not loading after moving game from one drive to another.

## 🚨 Problem Description

After moving DST using Steam's **Move Install Folder** feature:
- Only a subset of Workshop mods loads correctly
- Other subscribed mods appear as **incompatible**, show placeholder entries, or do not appear in the in-game Mods list
- Steam still shows the mods as subscribed, but DST does not load their actual content

The same set of mods worked correctly **before** the move.  
The issue starts immediately **after** the Steam move operation.

**Root Cause**: Steam updates the game installation path, but DST’s Workshop resolution logic may continue to reference stale paths from the previous drive.

## 🔧 Workaround (Manual Recovery)

This workaround reconstructs a stable local mod state without relying on DST’s broken Workshop resolution.

### 1. Backup existing Workshop mods

Locate Steam Workshop content: `steamapps/workshop/content/322330`

For each mod directory:

- Copy it to a temporary backup folder
- Rename it with the `workshop_` prefix  
  Example: `workshop_123456789`
  
### 2. Prepare DST mods directory

Go to: `steamapps/common/Don't Starve Together/mods`

- Temporarily set the folder to **read-only**
- Launch DST once, then exit  
  (Steam may reset permissions, but copied folders will remain)

### 3. Reset Steam subscriptions

- Unsubscribe from **all** DST Workshop mods in Steam
- Launch DST once to clear cached mod state
- Exit the game

### 4. Re-subscribe critical mods

- Re-subscribe only to the mods that must stay managed by Steam
- Launch DST and verify these mods now load correctly
- Confirm their Workshop folders contain full data (not empty / legacy-only)

### 5. Restore remaining mods manually

- Copy the backed-up `workshop_xxx` folders into: `steamapps/common/Don't Starve Together/mods`
- Do **not** re-subscribe these mods in Steam

### 6. Verify

- Launch DST
- All restored mods should appear and load correctly
- Steam-managed mods will update normally
- Manually restored mods remain stable but will not auto-update

### ⚠️ Notes and Limitations

- Manually installed mods will **not receive Steam updates**.
- Updating those mods requires repeating parts of this process.

This state is stable and avoids DST repeatedly resolving Workshop paths incorrectly after a Steam move.

---

This document records the workaround as a reproducible recovery procedure rather than a permanent fix.
