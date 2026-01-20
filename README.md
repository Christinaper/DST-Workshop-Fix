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

**Observed behavior**: After moving the game via Steam, DST shows inconsistent Workshop mod loading. While Steam updates the game installation path, some Workshop metadata or local resolution state may remain out of sync, causing DST to misinterpret or ignore valid mod data.

## 🔧 Recovery Procedure (What Worked For Me)

### Prerequisites
- **Full backup of your save files** (do this first!)
- Admin/write permissions for Steam directories
- Time to test each step incrementally
- Pen and paper to note which mods fail in step 2

### Step-by-step Process

#### Step 1: Backup ALL existing mod data

**Scan both possible mod locations:**
```
Location A: steamapps/workshop/content/322330/
Location B: steamapps/common/Don't Starve Together/mods/
```

**For each mod folder that contains actual content** (not just empty folders or placeholder files):
```
Action: Copy the folder to a safe backup location
Rename: [folder_name] → workshop_[mod_id]

Examples:
  378160973/ → workshop_378160973/
  workshop-378160973/ → workshop_378160973/
```

**Critical**: After this step, you have a complete backup of all working mod content, regardless of which path they were originally in.

---

#### Step 2. Expose mod loading failures
```
- Navigate to: steamapps/common/Don't Starve Together/mods/
- Set folder to read-only (temporary)
- Launch DST → Check the in-game mod menu
- Note down which mods fail to load or show as "incompatible"
```

**Write down the mod IDs that failed** - these are the mods broken by the Steam move.

---

#### Step 3. Identify broken mods (Frozen local candidates)

**These mods MUST become frozen local mods:**
- Mods that failed to load in step 2
- Mods showing as "incompatible" in DST's mod menu
- Mods with empty/incomplete folders in `workshop/content/322330/` but have full content in your backup

**This is not a choice** - these mods are broken by the Steam move and cannot work through Steam Workshop anymore. They must be restored as local mods to function.

---

#### Step 4: Restore frozen local mods

**For each broken mod identified in step 3:**
```
Copy workshop_[mod_id]/ from your backup to:
  steamapps/common/Don't Starve Together/mods/

Keep the workshop_ prefix in the folder name
Do NOT touch Steam subscriptions yet
```

**Verify restoration:**
```
Launch DST
All restored mods should now appear in the mod list
These mods are now running as "local mods" bypassing Steam Workshop
Exit DST
```

---

#### Step 5: Clean up Steam subscriptions for frozen mods

**Now unsubscribe the restored mods from Steam:**
```
Go to Steam Workshop in your web browser or Steam client
Unsubscribe ONLY the mods you restored in step 4
Keep subscriptions active for mods that still work normally
```

**Why this order matters:**
- If you unsubscribe first, Steam might delete the mod folders
- By restoring first, you ensure the content is safe before removing Steam's broken reference

---

#### Step 6: Verify final state

**Launch DST and confirm:**
```
✓ All mods appear in the mod list
✓ Frozen local mods (unsubscribed from Steam) still work
✓ Steam-managed mods (still subscribed) continue to auto-update
```

**Create a record of frozen mods:**
```
Create a text file: frozen_mods_list.txt

List the mod IDs and names that you unsubscribed in step 5

Example:
  workshop_378160973 - Global Positions
  workshop_458940297 - Too Many Items
  workshop_375850593 - Geometric Placement
  
This helps you remember which mods won't auto-update
```

---

## ⚠️ Critical Limitations

**Understanding the two-tier mod system:**

After this procedure, your mods exist in two categories determined by what broke during the Steam move:

| Type | How They Got Here | Characteristics |
|------|-------------------|-----------------|
| **Steam-managed mods** | Mods that **survived the Steam move** | • Still subscribed in Steam<br>• Auto-update works normally<br>• Located in `workshop/content/322330/`<br>• May break again if Steam moves files |
| **Frozen local mods** | Mods that **broke during Steam move** | • Unsubscribed from Steam<br>• No auto-update (frozen at current version)<br>• Located in `DST/mods/workshop_xxx/`<br>• Immune to future Steam Workshop path issues<br>• **Must manually update** when needed |

**This distinction is determined by what broke, not by user preference.**

---

### Updating Frozen Local Mods

When you need to update a frozen local mod:

1. Find the mod on Steam Workshop
2. Check the "Change Notes" or update date
3. If an update is critical:
   - Temporarily re-subscribe in Steam
   - Let Steam download the updated version
   - Copy the updated folder and rename with `workshop_` prefix
   - Move to `DST/mods/` replacing the old version
   - Unsubscribe again from Steam

**Trade-off**: You sacrifice auto-update convenience for guaranteed stability.

---

## 🤔 Should You Try This?

**Consider this workaround if:**
- ✅ You've already moved your Steam installation and mods are broken
- ✅ Only Workshop mods are affected (base game works fine)
- ✅ You're comfortable with manual file operations
- ✅ You understand this creates a hybrid managed/unmanaged mod state

**Avoid this if:**
- ❌ Your mods still work fine after the move (no need to fix what isn't broken)
- ❌ You play on multiple machines with Steam Cloud
- ❌ You're uncomfortable manually managing files
- ❌ You need all mods to stay perfectly in sync with Workshop versions

---

## 📝 Alternative Approaches to Explore

Before trying this workaround, consider these simpler options:

1. **Steam's "Verify Integrity of Game Files"**
   - Right-click DST in Steam → Properties → Installed Files → Verify
   - Sometimes resolves Workshop path issues automatically

2. **Complete clean reinstall**
   - Slower but guarantees fresh Workshop subscriptions
   - Backup saves first: `Documents/Klei/DoNotStarveTogether/`

3. **Symlinks (Advanced)**
   - Create symbolic links to redirect Workshop paths
   - Requires command-line knowledge

4. **Wait for DST update**
   - Klei may fix Workshop path resolution in future patches
   - Check community forums for official responses

---

## 🔄 Updates and Maintenance

**This document reflects my experience as of [20/01/2026].**

If you find better solutions or encounter issues with this approach:
- Open an issue describing your specific case
- Share your system configuration:
  - Operating System
  - Steam library structure (single drive vs. multiple libraries)
  - Number of mods affected
  - Which step failed (if any)

I'll update this document if patterns emerge or better solutions are discovered.

---

📋 Quick Reference Checklist

- [ ] Backed up save files
- [ ] Scanned both mod locations (workshop/content and DST/mods)
- [ ] Backed up all mod folders with content → renamed to workshop_xxx
- [ ] Launched DST to identify which mods fail to load
- [ ] Noted down broken mod IDs
- [ ] Restored broken mods to DST/mods/ folder
- [ ] Verified restored mods work in DST
- [ ] Unsubscribed restored mods from Steam Workshop
- [ ] Created frozen_mods_list.txt for future reference
- [ ] Confirmed all mods load correctly in final state

---

**Final reminder**: This workaround trades auto-update convenience for stability. It's a conscious technical debt that requires manual maintenance. The two-tier system exists because Steam broke specific mods during the move - this procedure simply works around that breakage rather than fixing Steam's underlying path resolution issue.

**Keep your frozen_mods_list.txt safe** - you'll need it to know which mods require manual updates in the future.
