Master prompt for OpenCode/Claude Code CLI


**Objective:** Build a TypeScript app using Temporal to orchestrate the entire build pipeline.

**App spec:**
`{Describe your app here. Example: "Vite + React + TypeScript chatbot. Backend: Supabase. Inference: OpenAI API. Folder: /app-chat"}`


Workflow spec in mermaid:
```mermaid

sequenceDiagram
    autonumber
    participant WF as BuildAppWorkflow
    participant A1 as scaffoldRepo
    participant A2 as installDeps
    participant A3 as typeCheck  
    participant A4 as lint
    participant A5 as build

    WF->>A1: Create/update /app-chat per spec
    A1-->>WF: files written
    WF->>A2: pnpm install
    A2-->>WF: node_modules ready
    
    loop max 3 attempts
        WF->>A3: tsc --noEmit
        alt TS Error
            A3-->>WF: error message
            WF->>A1: retry with error context
            A1-->>WF: files patched
        else TS Success
            A3-->>WF: ok
            WF->>A4: eslint .
            alt Lint Error
                A4-->>WF: error message
                WF->>A1: retry with error context
                A1-->>WF: files patched
            else Lint Success
                A4-->>WF: ok
                WF->>A5: vite build
                alt Build Error
                    A5-->>WF: error message
                    WF->>A1: retry with error context
                    A1-->>WF: files patched
                else Build Success
                    A5-->>WF: dist/ ready
                end
            end
        end
    end


**Requirements:**
Parse the Mermaid diagram above and implement it as real Temporal code.
Create `/workflows/build-app.ts`, `/activities.ts`, `/worker.ts`

Each Mermaid step = one Activity. Use `@temporalio/workflow` + `@temporalio/worker`.

Retry policy: max 3 attempts for `installDeps`, `typeCheck`, `lint`, `build`. Set `scheduleToCloseTimeout` appropriately per activity (e.g. 2m for typeCheck/lint, 5m for build).

If `typeCheck`, `lint`, or `build` fails → loop back to `scaffoldRepo` and pass the **exact error string** as `previousError` so only that error gets fixed.

**`scaffoldRepo` Activity:** Generate all code here using the app spec + any SOP/PRD context. If `previousError` is provided, fix **only** that specific error — do not rewrite everything.

Do **not** start a dev server inside Temporal. Workflow ends when `vite build` succeeds and returns the `/app-chat/dist` path.

After writing the Temporal code, **start the Worker first, then trigger `BuildAppWorkflow` automatically.**

I will run `cd app-chat && pnpm dev` manually after Workflow success to test the UI at `localhost:5173`.

**Stack:** Vite + React + TypeScript + pnpm. Target folder: `/app-chat`

**Begin.**


