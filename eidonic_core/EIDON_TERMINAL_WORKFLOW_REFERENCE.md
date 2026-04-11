# EIDON TERMINAL WORKFLOW REFERENCE
**Platform:** Windows PowerShell  
**Repo root:** `C:\eidonic_core`  
**Current phase:** Phase 2 scaffold with chain, session persistence, artifact persistence, and artifact lineage

---

## 1. Core rules

- Work from `main` unless you are actively building a feature branch.
- After a PR is merged on GitHub, **update local first**.
- Use **terminal for local work** and **GitHub web UI for PR creation/merge** unless you later adopt GitHub CLI.
- Do not manually drag files into `C:\eidonic_core` once the repo is under Git control.
- Local JSON runtime files are not source code. Clean them before handoff if needed.

---

## 2. Check your current repo state

Run this any time you feel lost:

```powershell
cd C:\eidonic_core
git branch --show-current
git status
git branch -vv
```

---

## 3. Standard "update local after merge" flow

Run this after **every PR merge** before testing or starting the next branch:

```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git status
```

Expected clean result:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

## 4. Start a new feature branch

Always start from updated `main`:

```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git switch -c phase-2/your-branch-name
git branch --show-current
```

---

## 5. Commit and push a feature branch

After you make local file changes:

```powershell
cd C:\eidonic_core
git status
git add .
git commit -m "Your commit message here"
git push -u origin phase-2/your-branch-name
```

Safer explicit version when only certain files should be staged:

```powershell
cd C:\eidonic_core
git status
git add .\path\to\file1 .\path\to\file2 .\path\to\file3
git commit -m "Your commit message here"
git push -u origin phase-2/your-branch-name
```

---

## 6. After branch push

Terminal is done. Then use GitHub web UI to:

1. Open the PR
2. Review it
3. Merge it
4. Delete the remote branch

Then come back to terminal and do Section 3: **update local after merge**.

---

## 7. Start the full Phase 2 stack from one command

This is the normal way to turn on the current services:

```powershell
cd C:\eidonic_core
powershell -ExecutionPolicy Bypass -File .\scripts\start_phase_2_stack.ps1
```

This opens four PowerShell windows for:

- `herald-service` on port `8001`
- `session-engine` on port `8002`
- `eidon-orchestrator` on port `8003`
- `signal-gateway` on port `8000`

---

## 8. Start a single service manually

Use this when only one service changed and you do not want to restart the whole stack.

### Herald
```powershell
cd C:\eidonic_core\services\herald-service
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8001
```

### Session Engine
```powershell
cd C:\eidonic_core\services\session-engine
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8002
```

### Eidon Orchestrator
```powershell
cd C:\eidonic_core\services\eidon-orchestrator
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8003
```

### Signal Gateway
```powershell
cd C:\eidonic_core\services\signal-gateway
.\.venv\Scripts\python.exe -m uvicorn app.main:app --reload --port 8000
```

---

## 9. Reinstall dependencies when a service changed requirements

Do this after a merge that changed `requirements.txt` or added a package.

### Signal Gateway
```powershell
cd C:\eidonic_core\services\signal-gateway
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Herald
```powershell
cd C:\eidonic_core\services\herald-service
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Session Engine
```powershell
cd C:\eidonic_core\services\session-engine
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Eidon Orchestrator
```powershell
cd C:\eidonic_core\services\eidon-orchestrator
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

---

## 10. Create a missing virtual environment

Use this if a service does not have `.venv` yet:

### Signal Gateway
```powershell
cd C:\eidonic_core\services\signal-gateway
py -V:3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Herald
```powershell
cd C:\eidonic_core\services\herald-service
py -V:3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Session Engine
```powershell
cd C:\eidonic_core\services\session-engine
py -V:3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

### Eidon Orchestrator
```powershell
cd C:\eidonic_core\services\eidon-orchestrator
py -V:3.12 -m venv .venv
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
```

---

## 11. Run the current full integration test

Current test verifies:
- full chain response
- session persistence
- artifact persistence

Run from repo root:

```powershell
cd C:\eidonic_core
powershell -ExecutionPolicy Bypass -File .\tests\integration\test_full_chain.ps1
```

Expected success ending:

```text
Full chain integration test with session and artifact persistence passed.
```

---

## 12. Manually trigger the full chain

Use this to hit the whole chain through `signal-gateway`:

```powershell
cd C:\eidonic_core\services\signal-gateway
$body = Get-Content .\examples\sample_signal_event.json -Raw
$response = Invoke-RestMethod -Uri "http://127.0.0.1:8000/signals/ingest" `
  -Method Post `
  -ContentType "application/json" `
  -Body $body
$response | ConvertTo-Json -Depth 12
```

This should return nested:
- `herald_result`
- `session_result`
- `eidon_result`

And currently should also include:
- `derived_intent`
- `artifact_id`
- `lineage_id`

---

## 13. Retrieve a persisted session directly

Known sample session id:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8002/sessions/session-sig-001" `
  -Method Get | ConvertTo-Json -Depth 12
```

---

## 14. List persisted sessions

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8002/sessions" `
  -Method Get | ConvertTo-Json -Depth 12
```

---

## 15. Retrieve a persisted artifact directly

Known sample artifact id:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8003/artifacts/artifact-session-sig-001" `
  -Method Get | ConvertTo-Json -Depth 12
```

---

## 16. Retrieve artifact lineage directly

Known sample artifact id:

```powershell
Invoke-RestMethod -Uri "http://127.0.0.1:8003/lineage/artifact-session-sig-001" `
  -Method Get | ConvertTo-Json -Depth 12
```

---

## 17. Stop running services

In each open service window:

```text
Ctrl + C
```

Then close the window.

---

## 18. Clean local runtime JSON files for handoff

Use this when you want a clean working tree and do not want local runtime files hanging around:

```powershell
cd C:\eidonic_core
Remove-Item .\services\session-engine\data\sessions.json -Force -ErrorAction SilentlyContinue
Remove-Item .\services\eidon-orchestrator\data\artifacts.json -Force -ErrorAction SilentlyContinue
Remove-Item .\services\eidon-orchestrator\data\lineage.json -Force -ErrorAction SilentlyContinue
git status
```

Expected clean result:

```text
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```

---

## 19. Clean up a local branch after merge

After the PR is merged and remote branch deleted:

```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git branch -d phase-2/your-branch-name
```

If Git resists and you are sure it is safe:

```powershell
git branch -D phase-2/your-branch-name
```

---

## 20. Fix the "remote branch no longer exists" warning

If Git says your configuration specifies a deleted remote branch, switch back to `main` and pull:

```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git branch -vv
```

Then delete the stale local branch:

```powershell
git branch -d phase-2/old-branch-name
```

---

## 21. Daily safe working order

This is the normal rhythm.

### Start work
```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git status
```

### Create a feature branch
```powershell
git switch -c phase-2/your-branch-name
```

### Make changes, then commit and push
```powershell
git status
git add .
git commit -m "Your commit message here"
git push -u origin phase-2/your-branch-name
```

### Merge on GitHub
Do this in the browser.

### Update local after merge
```powershell
cd C:\eidonic_core
git switch main
git pull --ff-only
git status
```

### Start stack
```powershell
cd C:\eidonic_core
powershell -ExecutionPolicy Bypass -File .\scripts\start_phase_2_stack.ps1
```

### Run integration test
```powershell
cd C:\eidonic_core
powershell -ExecutionPolicy Bypass -File .\tests\integration\test_full_chain.ps1
```

### Clean runtime files if needed
```powershell
cd C:\eidonic_core
Remove-Item .\services\session-engine\data\sessions.json -Force -ErrorAction SilentlyContinue
Remove-Item .\services\eidon-orchestrator\data\artifacts.json -Force -ErrorAction SilentlyContinue
Remove-Item .\services\eidon-orchestrator\data\lineage.json -Force -ErrorAction SilentlyContinue
git status
```

---

## 22. Current live chain

```text
signal-gateway -> herald-service -> session-engine -> eidon-orchestrator
```

---

## 23. Current verified persistence

- `SessionRecord` via local JSON
- `EidonArtifactRecord` via local JSON
- `ArtifactLineageRecord` via local JSON

---

## 24. Current discipline

- terminal-only for local work
- update local after every merge
- no live model in runtime yet
- persistence and lineage architecture before model runtime integration
