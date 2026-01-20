# DST Mod Fix After Steam Move – Workaround

> **⚠️ This is a workaround record, not a universal solution**  
> This document captures a specific recovery procedure that worked in my case. Due to varying system configurations, Steam library structures, and mod dependencies, **this may not work for everyone**. Treat this as a reference point for troubleshooting, not a guaranteed fix.

---

## 🚨 Problem Context

**Scenario**: After moving *Don't Starve Together* using Steam's **Move Install Folder** feature:
- Only partial Workshop mods loads correctly
- Other subscribed mods show as **incompatible** or missing
- Steam subscription status appears normal
- Issue persists across game restarts

**Root Cause hypothesis**: Steam updates installation paths, but DST’s Workshop resolution logic may cache or reference stale paths from the previous drive location.

## 🔧 Recovery Procedure (What Worked For Me)

### Prerequisites
- Full backup of your save files (do this first!)
- Admin/write permissions for Steam directories
- Time to test each step incrementally

### Step-by-step Process

### 1. Archive existing Workshop data
```
Location: steamapps/workshop/content/322330/
Action: Copy each mod folder to backup location
Rename: [original_id] → workshop_[original_id]
Example: 123456789 → workshop_123456789
```

### 2. Force DST to recognize path changes
```
Navigate to: steamapps/common/Don't Starve Together/mods/
Set folder to read-only (temporary)
Launch DST → Exit immediately
(This triggers DST's internal path verification)
```

### 3. Clear Steam's cached subscription state
```
Unsubscribe from ALL DST Workshop items
Launch DST once (to flush mod cache)
Exit game
```

### 4. Re-subscribe critical mods
```
Re-subscribe ONLY to the mods that must stay managed by Steam
Launch DST and verify these mods load correctly
Check Workshop folders contain full content (not just .upd / legacy-only files)
```

### 5. Restore remaining mods manually
```
Copy steamapps/Workshop/Content/322330 remaining mods and rename: [original_id] → workshop_[original_id] folders to: steamapps/common/Don't Starve Together/mods/
Do NOT re-subscribe these in Steam
Launch DST and verify all mods appear in-game
```

---

## ⚠️ Critical Limitations

**This is a stable state, not a permanent solution:**

| Aspect | Impact |
|--------|--------|
| **Manually restored mods** | Will NOT auto-update from Workshop |
| **Updates required** | Manual re-download and replacement |
| **Path dependencies** | Your Steam library structure may differ significantly |
| **Mod compatibility** | Some mods may have server-sync requirements |
| **Future Steam operations** | Moving/verifying files may break this state again |

**Why this works (in my case)**: By isolating mods from Steam's Workshop resolution, DST reads them as local mods, bypassing the path confusion that occurred after the move.

---

## 🤔 Should You Try This?

**Consider this workaround if:**
- ✅ You've already moved your Steam installation
- ✅ Only Workshop mods are affected (base game works)
- ✅ You're comfortable with manual file operations
- ✅ You understand this creates a hybrid managed/unmanaged mod state

**Avoid this if:**
- ❌ You need all mods to auto-update
- ❌ You play on multiple machines with Steam Cloud
- ❌ Your mods are server-authoritative (may cause version conflicts)
- ❌ You're not familiar with Steam directory structures

---

## 📝 Alternative Approaches to Explore

Before trying this workaround, consider:

1. **Steam's "Verify Integrity of Game Files"** - Sometimes resolves Workshop subscriptions
2. **Complete clean reinstall** - Slower but more reliable for some users
3. **Symlinks** - Advanced users might redirect Workshop paths directly
4. **Wait for DST update** - Klei may fix Workshop path resolution in future patches

---

## 🔄 Updates and Maintenance

**This document reflects my experience as of [20/01/2026].**

If you find better solutions or encounter issues with this approach:
- Open an issue describing your specific case
- Share your system configuration (OS, Steam library setup, mod count)
- I'll update this doc if patterns emerge

---

**Final reminder**: This workaround trades auto-update convenience for stability. It's a conscious technical debt that requires manual maintenance. Document which mods you've manually installed vs. Steam-managed to avoid future confusion.
