Got it — here’s the exact sequence between you, minimax, and Temporal.

sequenceDiagram
    autonumber
    participant Human as Human
    participant Agent as OpenCode minimax
    participant Server as Temporal Server<br/>localhost:7233
    participant Worker as Temporal Worker<br/>pnpm start

    Human->>Server: Run temporal.exe server start-dev
    Server-->>Human: Server + UI ready on :7233 / :8233
    
    Human->>Agent: Paste master prompt in D:\xyz
    Agent->>Agent: Create package.json, tsconfig.json
    Agent->>Agent: Create activities.ts, workflows/build-app.ts, worker.ts
    Agent->>Worker: Run pnpm start
    Worker->>Server: Connect to localhost:7233
    Worker->>Server: Start BuildAppWorkflow
    Server->>Worker: Schedule scaffoldRepo activity
    Worker->>Worker: Execute scaffoldRepo → create D:\xyz\app-chat
    Worker->>Server: Report activity success
    Server->>Worker: Schedule installDeps, typeCheck, lint, build...
    loop until vite build succeeds
        Worker->>Worker: Run activity
        Worker->>Server: Return result/error
        Server->>Worker: Schedule next or retry scaffoldRepo
    end
    Worker->>Server: Workflow completed: dist/ ready
    Server-->>Worker: Success
    Worker-->>Agent: Log: Workflow completed
    Agent-->>Human: "Done. Run cd app-chat && pnpm dev"

Key takeaways

Human only does 2 things: start Temporal server, then test with pnpm dev at the end
minimax agent does all file creation + runs pnpm start 
Temporal Server orchestrates the loop. It remembers state so retries work
Worker is just a process on your machine that executes activities when Server tells it to

This is why you can kill pnpm start and restart it — the workflow resumes where it left off because Temporal Server saved the state.

Ready to run it?
