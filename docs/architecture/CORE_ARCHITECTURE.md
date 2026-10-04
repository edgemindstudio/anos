# ANOS Core Architecture

```text
                         ANOS
          Agentic Native Operating System

 ┌─────────────────────────────────────────┐
 │ Native identity model                   │
 │   ├── human principals                  │
 │   ├── system principals                 │
 │   └── agent principals                  │
 │                                         │
 │ Native execution model                  │
 │   ├── processes                         │
 │   ├── threads                           │
 │   └── agents                            │
 │                                         │
 │ Native authority model                  │
 │   ├── permissions                       │
 │   ├── capabilities                      │
 │   └── delegation                        │
 │                                         │
 │ Native security model                   │
 │   ├── isolation                         │
 │   ├── policy enforcement                │
 │   ├── revocation                        │
 │   └── trust boundaries                  │
 │                                         │
 │ Native resource model                   │
 │   ├── CPU / memory / GPU                │
 │   ├── agent budgets                     │
 │   └── model / token resources           │
 │                                         │
 │ Native scheduling model                 │
 │   ├── process/thread scheduling         │
 │   ├── agent scheduling                  │
 │   ├── heterogeneous resources           │
 │   └── priorities / deadlines / budgets  │
 │                                         │
 │ Native memory model                     │
 │   ├── virtual memory                    │
 │   ├── agent working memory              │
 │   ├── persistent agent state            │
 │   └── protected/shared agent memory     │
 │                                         │
 │ Native communication model              │
 │   ├── IPC                               │
 │   └── agent communication               │
 │                                         │
 │ Native lifecycle model                  │
 │   ├── process lifecycle                 │
 │   └── agent lifecycle                   │
 │                                         │
 │ Native observability                    │
 │   ├── process auditing                  │
 │   └── agent/delegation auditing         │
 │                                         │
 │ Native accountability model             │
 │   ├── action provenance                 │
 │   ├── delegation lineage                │
 │   ├── resource accounting               │
 │   └── responsibility attribution        │
 └─────────────────────────────────────────┘
```

## Execution relationship

```text
                     ANOS
                      │
              Execution Substrate
                      │
        ┌─────────────┴─────────────┐
        │                           │
     Process                      Agent
        │                           │
     Threads                 Agent Control State
                                    │
                     ┌──────────────┼──────────────┐
                     │              │              │
                 Processes        Tools        Sub-agents
```

## Delegation relationship

```text
Human / Organization / System Principal
                  │
           delegates authority
                  ▼
                Agent
                  │
           delegates subset
                  ▼
              Sub-agent
                  │
          executes processes/tools
```

ANOS must preserve provenance across this entire chain.
