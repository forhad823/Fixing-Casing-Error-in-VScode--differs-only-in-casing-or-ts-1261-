# Fixing-Casing-Error-in-VScode--differs-only-in-casing-or-ts-1261-

## Casing Error Fix — One Path

```
↓  Read the error → spot "differs only in casing" or ts(1261)

↓  Compare the two paths in the error message
      import says  →  src/Routes/Router.jsx
      disk has     →  src/routes/router.jsx

↓  Pick one casing and stick to it (whole project)

↓  Rename on disk safely (Windows two-step trick)
      routes  →  routes_temp  →  Routes

↓  Update every import to match the new name exactly

↓  Ctrl+Shift+P  →  TypeScript: Restart TS Server

↓  Still showing? → Ctrl+Shift+P  →  Developer: Reload Window

↓  Done — red marker gone
```
### What triggers this type of error?

Any time you **rename a file or folder** and only change the casing (e.g., `Routes` → `routes`, `Components` → `components`), on a **Windows or macOS** machine.

---

### Step-by-Step Fix Process

**Step 1 — Read the error message carefully**

Look for keywords like:
- *"differs from file name only in casing"*
- *"Already included file name"*
- `ts(1261)`

This immediately tells you it's a **case mismatch**, not a logic bug.

**Step 2 — Find the conflict**

The error message itself tells you both paths. Compare them:
```
'src/Routes/Router.jsx'   ← what the import says
'src/routes/router.jsx'   ← what's actually on disk
```
Spot the difference in casing.

**Step 3 — Pick ONE consistent casing and stick to it**

Either all lowercase (`routes/router.jsx`) or capitalized (`Routes/Router.jsx`) — just be consistent across your whole project. Then fix **both sides**:

- The actual file/folder name on disk
- Every `import` statement that references it

**Step 4 — Rename safely on Windows**

Windows won't register a rename that only changes case if you do it directly. Use this two-step trick:

```
routes  →  routes_temp  →  Routes
```
Rename to a temp name first, then rename again to your desired casing. This forces the OS to recognize it as a real rename.

**Step 5 — Restart the TS Server**

Even after fixing, VS Code may still show the error due to stale cache:
```
Ctrl + Shift + P  →  "TypeScript: Restart TS Server"
```

If still showing, also try:
```
Ctrl + Shift + P  →  "Developer: Reload Window"
```

---

### Quick Mental Checklist

| Check | Question to ask |
|---|---|
| 📁 Disk name | What is the **exact** folder/file name on disk? |
| 📝 Import path | Does every import **exactly match** the disk name in casing? |
| 🔄 Renamed recently? | Did you only change casing? Use the two-step rename trick. |
| 🧹 Cache cleared? | Did you restart the TS Server after fixing? |

---

### Prevention Tips

- Agree on a naming convention at the start — most React projects use **PascalCase** for components (`MyComponent.jsx`) and **camelCase/lowercase** for folders (`routes/`, `hooks/`, `utils/`).
- If using Git, run `git config core.ignorecase false` so Git also tracks case changes properly.
- Treat casing errors **the same as typos** — they're real errors even if Windows masks them.
