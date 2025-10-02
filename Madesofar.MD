## summary for reference 
##

Prereqs (one-time)
Install: Azure Developer CLI, Python 3.9–3.11, Node.js 20+, Git, PowerShell 7+ (pwsh)
Ensure you can run pwsh, python --version, node -v, and azd version.
Provision once (required before local run)
Run these from the repo root in PowerShell 7+ (pwsh):

azd auth login
azd env new
azd up

Start locally (build frontend once, backend auto-reloads)
From the repo root in PowerShell 7+:
This loads your azd environment variables, creates .venv, installs backend deps, runs npm install and npm run build for the frontend, and starts the backend with auto-reload at http://127.0.0.1:50505.
Open http://127.0.0.1:50505 in your browser.

Hot reloading (frontend + backend)
Keep the backend running as above (it auto-reloads on Python file changes).
In a second terminal:
Open the Vite URL it prints (typically http://localhost:5173/). Frontend HMR will proxy API calls to the Python backend.


VS Code options (optional)
Run the task “VS Code Task: Start App”, or use the launch configurations “Frontend”, “Backend (Python)”, or “Frontend & Backend” in .vscode/launch.json.
If you need to adjust environment values locally (like model or search settings), use:
then restart the local server.
To stop: Ctrl+C in the terminals or terminate VS Code tasks.
Default ports: backend 50505, frontend dev 5173.
If you see errors loading env vars, make sure you ran azd up and that you’re using PowerShell 7+ (pwsh), not Windows PowerShell 5.1.

Docs for reference: docs/localdev.md and the script app/start.ps1.
Built frontend from start.ps1 isn’t hot-reloaded; use npm run dev for HMR.
If Node or Python path issues occur on Windows, ensure both are on PATH and re-open your terminal.
Clean rebuild tip: delete .venv and app/frontend/node_modules, then re-run ./app/start.ps1.
For local model experimentation, see the “Using a local OpenAI-compatible API” section in docs/localdev.md.

If you encounter port conflicts, stop any existing processes on 50505/5173 or change ports in vite.config.ts and backend start command.