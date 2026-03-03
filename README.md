# linux-bootcamp-notes

Notes + scripts + 1-page command sheet from my Linux bootcamp (WSL Ubuntu).

## Contents
- `notes/` — week-by-week notes
- `cheatsheets/linux-command-sheet.md` — 1-page commands I actually use
- `scripts/` — small utilities written during practice

## Scripts

### 1) mkproj.sh
Creates a standard project folder tree.
```bash
bash scripts/mkproj.sh my_project
```

### 2) collect_logs.sh
Collects system/log info into a timestamped bundle.
```bash
bash scripts/collect_logs.sh --out out/
```

### 3) search_tree.sh
Searches a directory tree with filters.
```bash
bash scripts/search_tree.sh --root . --name "*.txt" --contains "error"
```
