# Agentic Software Engineering Guide

A practical map of how software teams use AI coding agents.

AI coding agents are becoming part of everyday development work. They can read repositories, edit files, run commands, run tests, call tools, use sandboxes, create branches, open pull requests, and help prepare changes for review.

This guide explains the main concepts behind that shift. It is a living map of the field, covering established standards, documented product features, open-source frameworks, and practical engineering patterns that are still emerging.

It is not tied to one vendor, framework, or workflow. The goal is to make agentic software engineering easier to understand by separating the recurring methods, lifecycle stages, building blocks, tools, protocols, runtime patterns, evaluation practices, and governance controls that software teams increasingly rely on when working with AI coding agents.

## What this guide covers

* How teams work with AI coding agents
* Where agents fit in the software delivery lifecycle
* Tools, products, and frameworks used for agentic development
* Building blocks such as instructions, tools, skills, memory, hooks, sandboxes, and evals
* Protocols that let agents, tools, editors, and apps connect
* Runtime infrastructure for running agents safely
* Patterns for delegation, review, repair, and verification
* Observability, evaluation, security, governance, and reproducibility
* Packaging approaches for sharing agent capabilities across teams and repositories

## Why this exists

Agentic software engineering introduces many new moving parts.

This guide separates the standards, product features, frameworks, patterns, and early ideas that make up the field, so engineers can understand them, compare them, and discuss them more clearly.

## Mental model

Agentic software engineering is not one tool or one workflow. It is a stack of concepts that fit together.

```text
How teams work
  -> Where agents fit in the lifecycle
    -> Tools and frameworks
      -> Building blocks
        -> Protocols
          -> Runtime infrastructure
            -> Discovery and distribution
              -> App and developer surfaces
                -> Execution patterns
                  -> Observability
                    -> Evaluation
                      -> Security and governance
                        -> Supply chain and reproducibility
                          -> Packaging
```

Each part answers a different question.

| Area                       | Question it answers                                                    |
| -------------------------- | ---------------------------------------------------------------------- |
| Methods                    | How should humans and agents build software together?                  |
| Lifecycle stages           | Where does the agent fit in the delivery process?                      |
| Tools and frameworks       | Which systems implement agentic workflows?                             |
| Building blocks            | What primitives does the agent use?                                    |
| Protocols                  | How do agents, tools, apps, editors, and runtimes connect?             |
| Runtime infrastructure     | Where and how does agent execution happen?                             |
| Discovery and distribution | How are agents, tools, skills, prompts, and packages found and shared? |
| App surfaces               | Where do humans inspect, approve, and interact with agentic work?      |
| Execution patterns         | How is work split, delegated, verified, repaired, and merged?          |
| Observability              | How do we see what the agent actually did?                             |
| Evaluation                 | How do we know whether the agent is useful, correct, and safe?         |
| Governance                 | How do we keep agentic work controlled and auditable?                  |
| Supply chain               | How do we track the dependencies and provenance of agentic work?       |
| Packaging                  | How do we share and reproduce agent capabilities?                      |

---

# 1. Methods and operating models

Methods describe how humans and agents structure software work together.

| Concept                                     | Meaning                                                                                                         |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| Spec-driven Development (SDD)               | Write requirements, architecture, acceptance criteria, and tasks before asking agents to implement.             |
| Structured-Prompt-Driven Development (SPDD) | Treat prompts as versioned engineering artifacts that can be reviewed, reused, and improved.                    |
| Agent-Centric Development Cycle (AC/DC)     | Guide the agent, let it generate, verify the result, then feed issues back into a repair loop.                  |
| Test-driven Agentic Development             | Give the agent tests, fixtures, and acceptance criteria so correctness can be checked automatically.            |
| Constitutional Agentic Development          | Encode non-negotiable rules, such as security, architecture, and compliance constraints, before implementation. |
| Context-driven Development                  | Give agents curated repository context instead of relying only on the latest prompt.                            |
| Human-governed Agentic Development          | Let agents do work, but require humans to approve sensitive actions.                                            |
| Review-driven Agentic Development           | Let agents move quickly, but gate progress through tests, traces, diffs, and review evidence.                   |
| Eval-driven Agentic Development             | Improve agents through repeatable evaluation suites and measurable quality signals.                             |
| Governance-driven Agentic Development       | Treat identity, access, audit logs, approval policy, and compliance as core parts of the workflow.              |

---

# 2. Lifecycle stages

These are common stages in agentic software work. Individual tools may combine, skip, or rename them.

| Stage             | What happens                                                                               |
| ----------------- | ------------------------------------------------------------------------------------------ |
| Intent capture    | A request, issue, incident, or product goal becomes a concrete engineering objective.      |
| Clarification     | The agent asks questions, checks assumptions, and narrows the scope.                       |
| Specification     | Requirements, constraints, risks, interfaces, and acceptance criteria are written down.    |
| Planning          | The agent breaks the work into tasks, files, tests, risks, and sequence.                   |
| Context assembly  | Relevant code, docs, tickets, dependency graphs, and prior decisions are gathered.         |
| Environment setup | The agent prepares the workspace, installs dependencies, and checks that commands can run. |
| Generation        | The agent writes code, tests, docs, configs, scripts, migrations, or pull request content. |
| Verification      | Tests, type checks, linters, scanners, policy checks, and review rules are run.            |
| Repair            | The agent fixes issues found during verification or review.                                |
| Review            | Humans or evaluator agents inspect the diff, trace, risks, and verification evidence.      |
| Integration       | Approved changes are committed, merged, released, deployed, or handed off.                 |
| Delivery          | The change moves through CI/CD, release automation, feature flags, or rollout gates.       |
| Maintenance       | Agents help update dependencies, repair regressions, refresh docs, and monitor drift.      |
| Retrospective     | The team reviews what worked, what failed, and what should improve.                        |

---

# 3. Tools, platforms, and frameworks

This section lists systems that implement parts of agentic software engineering.

## 3.1 Coding agents and agentic development tools

| Tool                         | What it does                                                                                      |
| ---------------------------- | ------------------------------------------------------------------------------------------------- |
| OpenAI Codex                 | Coding agent that can read, edit, and run code in local, IDE, or cloud environments.              |
| Claude Code                  | Agentic coding tool with memory, skills, hooks, MCP, subagents, worktrees, and permissions.       |
| GitHub Copilot Custom Agents | Specialized Copilot agents for team workflows, conventions, and tool access.                      |
| Cursor                       | AI-native code editor with repository-aware coding workflows.                                     |
| Windsurf                     | AI coding environment focused on repository context, code edits, and developer collaboration.     |
| Kiro                         | Agentic development environment focused on spec-driven development.                               |
| Devin                        | Long-running software engineering agent for planning, execution, testing, and progress reporting. |
| Factory Droids               | Cloud-based software agents that take assigned tasks and produce repository changes for review.   |
| CodeRabbit                   | Pull request review agent that summarizes diffs and leaves review feedback.                       |

## 3.2 Open-source software engineering agents

| Tool      | What it does                                                                                                        |
| --------- | ------------------------------------------------------------------------------------------------------------------- |
| OpenHands | Open-source software engineering agent platform with repository access, command execution, and isolated workspaces. |
| SWE-agent | Framework for using language models to inspect repositories, edit files, run tests, and fix GitHub issues.          |

## 3.3 Agent frameworks and orchestration SDKs

| Framework                          | What it helps with                                                                                  |
| ---------------------------------- | --------------------------------------------------------------------------------------------------- |
| OpenAI Agents SDK                  | Agents, tools, handoffs, guardrails, tracing, and human review.                                     |
| LangGraph                          | Durable execution, stateful workflows, streaming, human-in-the-loop, and long-running agents.       |
| LangChain Deep Agents              | Subagents, filesystem state, todos, middleware, and deeper agent workflows.                         |
| Microsoft Agent Framework          | Agents and multi-agent workflows with MCP support, checkpointing, telemetry, and human-in-the-loop. |
| Google Agent Development Kit (ADK) | Building, debugging, evaluating, and deploying agents and multi-agent systems.                      |
| CrewAI                             | Multi-agent crews, flows, memory, knowledge, guardrails, and observability.                         |

---

# 4. Building blocks

Building blocks are the reusable pieces that agents, tools, and workflows are made from.

## 4.1 Agent definition and instructions

| Building block              | Meaning                                                                                             |
| --------------------------- | --------------------------------------------------------------------------------------------------- |
| Agents / custom agents      | Model-driven workers with goals, instructions, tools, permissions, and context.                     |
| Agent manifests / AGENTS.md | Repository instruction files for setup commands, tests, conventions, and project guidance.          |
| Custom instructions         | Persistent guidance that shapes how an assistant or coding agent behaves.                           |
| Custom prompt files         | Reusable task prompts stored as files for code review, refactoring, docs, tests, and similar tasks. |
| Subagent profiles           | Named specialist agents with descriptions, instructions, tools, and optional output schemas.        |
| Typed subagent responses    | Structured outputs that make subagent results easier to validate, compare, and merge.               |

## 4.2 Skills, tools, and extensions

| Building block         | Meaning                                                                                                      |
| ---------------------- | ------------------------------------------------------------------------------------------------------------ |
| Skills                 | Packaged instructions and supporting files that teach an agent a repeatable capability.                      |
| Hooks                  | Commands, endpoints, or event handlers that run at specific lifecycle points.                                |
| Handoffs               | Passing a task from one agent to another while preserving context.                                           |
| Plugins                | Bundles of agent extensions such as skills, agents, hooks, MCP servers, or monitors.                         |
| Tools and tool calling | Schema-defined functions, APIs, commands, browsers, databases, or file operations the agent can call.        |
| MCP servers            | Servers that expose tools, resources, prompts, and external systems through MCP.                             |
| Resources              | Files, documents, APIs, databases, logs, traces, repository content, or retrieved context exposed to agents. |
| Prompts as resources   | Reusable prompt templates exposed by a server, package, repository, or framework.                            |
| Tool catalogs          | Lists of available tools with descriptions, schemas, permissions, risk levels, and usage guidance.           |

## 4.3 Context and state

| Building block                          | Meaning                                                                                            |
| --------------------------------------- | -------------------------------------------------------------------------------------------------- |
| Context / memory                        | Project conventions, user preferences, decisions, facts, and prior outputs carried across runs.    |
| Session state                           | Accumulated state from a longer agent interaction.                                                 |
| Long-term memory                        | Persisted knowledge used across sessions, repositories, or users.                                  |
| Scratchpads                             | Temporary working notes, plans, hypotheses, or partial findings.                                   |
| Context compaction                      | Summarizing or reducing accumulated context so long-running agents can continue.                   |
| Context anchors / repository blueprints | Durable project maps for architecture, ownership, domain concepts, constraints, and test surfaces. |
| Repository maps                         | Compact maps of files, modules, symbols, dependencies, and architecture.                           |
| Retrieval connectors                    | Components that fetch context from docs, code, tickets, logs, designs, or knowledge bases.         |

## 4.4 Planning and work units

| Building block      | Meaning                                                                                       |
| ------------------- | --------------------------------------------------------------------------------------------- |
| Plans / task graphs | Ordered or parallel task breakdowns that can be reviewed, executed, retried, or delegated.    |
| Todo lists          | Lightweight task state for tracking progress and remaining work.                              |
| Workflows           | Repeatable paths that combine model calls, tools, routing, verification, and human gates.     |
| Artifacts           | Durable outputs such as files, patches, dashboards, reports, screenshots, notebooks, or docs. |
| Patch sets          | Agent-generated file changes grouped as reviewable units.                                     |

## 4.5 Execution and control

| Building block                | Meaning                                                                                              |
| ----------------------------- | ---------------------------------------------------------------------------------------------------- |
| Runtime environment / sandbox | Isolated space where agents can inspect files, run commands, install dependencies, and test changes. |
| Permission profiles           | Rules for what an agent may read, edit, execute, install, call, approve, or publish.                 |
| Approval requests             | Requests asking a human or policy system to allow, deny, modify, or escalate risky actions.          |
| Checkpoints                   | Saved workflow state that lets an agent resume, retry, branch, or roll back.                         |
| Response schemas              | Structured output contracts for validating, filtering, merging, or scoring agent results.            |

## 4.6 Evaluation and provenance

| Building block               | Meaning                                                                                                 |
| ---------------------------- | ------------------------------------------------------------------------------------------------------- |
| Evaluation harnesses / evals | Test and measurement infrastructure for scoring agent behavior.                                         |
| Run records                  | Structured records of a single agent execution.                                                         |
| Provenance records           | Metadata linking agent actions, inputs, tools, files, prompts, commits, and approvals to final changes. |

---

# 5. Protocols and how tools connect

Protocols define how agents, tools, apps, editors, runtimes, and external systems communicate.

## 5.1 Agent-native protocols

| Protocol                                | What it helps with                                                                    |
| --------------------------------------- | ------------------------------------------------------------------------------------- |
| Model Context Protocol (MCP)            | Connecting AI apps and agents to tools, resources, prompts, and external systems.     |
| Agent2Agent Protocol (A2A)              | Letting agents discover each other, exchange tasks, communicate, and coordinate work. |
| Agent Client Protocol (ACP)             | Standardizing communication between editors, IDEs, and coding agents.                 |
| Agent User Interaction Protocol (AG-UI) | Streaming agent state and events between user-facing apps and agent backends.         |

## 5.2 Telemetry protocols and conventions

| Standard                                 | What it helps with                                                                                  |
| ---------------------------------------- | --------------------------------------------------------------------------------------------------- |
| OpenTelemetry Protocol (OTLP)            | Exporting traces, metrics, and logs into observability systems.                                     |
| OpenTelemetry GenAI semantic conventions | Standard names for GenAI model calls, tokens, prompts, tool calls, and agent steps.                 |
| OpenInference                            | OpenTelemetry-compatible tracing conventions for LLM calls, tools, retrievers, and agent workflows. |
| Trace context propagation                | Sharing correlation identifiers across agent runs, model calls, tools, gateways, and services.      |

## 5.3 API and schema standards

| Standard                        | What it helps with                                                                    |
| ------------------------------- | ------------------------------------------------------------------------------------- |
| JSON-RPC                        | Lightweight request and response messaging, often used by tool protocols.             |
| OpenAPI                         | Describing HTTP APIs so agents can understand available endpoints and schemas.        |
| JSON Schema                     | Defining tool arguments, validation rules, manifests, and structured outputs.         |
| OAuth / delegated authorization | Letting agents or tools access protected resources with bounded delegated access.     |
| Webhooks                        | Triggering agents from repository events, CI results, incidents, or external systems. |
| Event streams                   | Streaming ordered workflow, UI, tool, and agent events.                               |
| Server-Sent Events (SSE)        | Sending incremental updates from an agent backend to a client.                        |
| WebSockets                      | Bidirectional communication for interactive agent sessions.                           |
| gRPC                            | Typed service-to-service communication.                                               |
| GraphQL                         | Controlled access to structured application data.                                     |

## 5.4 Developer tooling standards

| Standard                       | What it helps with                                                             |
| ------------------------------ | ------------------------------------------------------------------------------ |
| Language Server Protocol (LSP) | Exposing diagnostics, symbols, references, completions, and code intelligence. |
| Debug Adapter Protocol (DAP)   | Exposing debugging actions and runtime state.                                  |
| SARIF                          | Sharing static analysis, security, and code scanning findings.                 |

## 5.5 Supply-chain standards

| Standard  | What it helps with                                                             |
| --------- | ------------------------------------------------------------------------------ |
| CycloneDX | Describing software components, dependencies, licenses, and supply-chain risk. |
| SPDX      | Describing software bill of materials, licenses, and supply-chain information. |

---

# 6. Runtime infrastructure and gateways

Runtime infrastructure describes where and how agents are executed, isolated, routed, observed, and controlled.

## 6.1 Gateways and routing

| Concept               | What it does                                                                                         |
| --------------------- | ---------------------------------------------------------------------------------------------------- |
| LLM gateways          | Proxy model calls, manage credentials, enforce budgets, redact data, and route requests.             |
| LangSmith LLM Gateway | Managed gateway for proxying LLM calls and managing provider access.                                 |
| MCP gateways          | Broker access between agents and MCP servers with auth, logging, rate limits, and policy.            |
| AI gateways           | Provide one API across model providers with routing, retries, fallbacks, budgets, and observability. |
| Tool brokers          | Mediate tool calls across APIs, MCP servers, internal services, and external systems.                |
| Model routers         | Select models based on cost, latency, capability, context length, reliability, or privacy.           |

## 6.2 Policy and access control

| Concept                          | What it does                                                                           |
| -------------------------------- | -------------------------------------------------------------------------------------- |
| Policy Enforcement Points (PEPs) | Intercept agent actions before execution and allow, deny, transform, or escalate them. |
| Secret and credential brokers    | Issue short-lived credentials so agents do not receive long-lived secrets.             |
| Approval services                | Manage human decisions for risky actions.                                              |
| Policy engines                   | Evaluate agent actions against rules, scopes, risks, and compliance requirements.      |

## 6.3 Execution environments

| Concept                             | What it does                                                                                    |
| ----------------------------------- | ----------------------------------------------------------------------------------------------- |
| Sandbox managers                    | Create isolated workspaces and control filesystem, network, and artifact access.                |
| Code interpreters for orchestration | Let agents run small programs for loops, branching, filtering, and subagent dispatch.           |
| Remote workspaces                   | Cloud or server-side environments where agents can clone repos, run tests, and produce changes. |
| Ephemeral environments              | Short-lived environments for a single task, run, pull request, or evaluation.                   |
| Persistent environments             | Longer-lived workspaces that preserve state across sessions.                                    |
| Network sandboxes                   | Limit which hosts, APIs, databases, or services an agent can reach.                             |
| Filesystem sandboxes                | Limit which files and directories an agent can read, write, or delete.                          |
| Command allowlists                  | Specify which commands, package managers, scripts, or binaries an agent may execute.            |

## 6.4 Runtime operations

| Concept               | What it does                                                                                   |
| --------------------- | ---------------------------------------------------------------------------------------------- |
| Execution queues      | Manage asynchronous jobs, retries, priorities, concurrency, and cancellation.                  |
| Run schedulers        | Decide when agent jobs start, pause, resume, retry, or stop.                                   |
| Cancellation controls | Let users or policy systems stop an agent run.                                                 |
| State stores          | Persist run metadata, session state, memory, tool outputs, traces, artifacts, and checkpoints. |
| Artifact stores       | Store generated files, patches, logs, test outputs, reports, and screenshots.                  |
| Replay engines        | Replay traces, tool calls, evaluations, or workflows to debug or compare versions.             |
| Dependency caches     | Speed up repeated agent runs while keeping environments reproducible.                          |

---

# 7. Discovery and distribution

Discovery and distribution describe how reusable agent capabilities are published, found, trusted, installed, and updated.

| Concept                | Meaning                                                                                                           |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------- |
| MCP registries         | Catalogs for publishing, finding, verifying, and installing MCP servers.                                          |
| Agent registries       | Catalogs of reusable agents with metadata about purpose, tools, permissions, owners, and versions.                |
| Skill registries       | Catalogs for reusable skills, prompts, instructions, scripts, and workflow modules.                               |
| Plugin registries      | Distribution channels for bundles of skills, agents, hooks, MCP servers, monitors, and policies.                  |
| Prompt registries      | Versioned catalogs of reusable prompts and task templates.                                                        |
| Workflow registries    | Catalogs of reusable multi-step workflows with routing, tools, gates, and verification logic.                     |
| Server manifests       | Metadata files describing a server, tools, resources, auth, capabilities, versions, and install steps.            |
| Agent cards            | Capability descriptions that explain what an agent can do and how to contact it.                                  |
| Package manifests      | Files that list agent dependencies, skills, prompts, tools, hooks, plugins, and MCP servers.                      |
| Lockfiles              | Files that pin exact dependency versions, commits, hashes, or resolved package trees.                             |
| Marketplace catalogs   | Places where teams browse, install, rate, audit, and update agent packages.                                       |
| Provenance metadata    | Metadata for source repositories, maintainers, signatures, hashes, licenses, and trust information.               |
| Capability indexes     | Searchable indexes of what agents, tools, MCP servers, skills, and workflows can do.                              |
| Trust registries       | Lists of approved packages, servers, agents, publishers, or tools.                                                |
| Deprecation metadata   | Signals that an agent, package, prompt, skill, plugin, or server is outdated or unsafe.                           |
| Compatibility metadata | Information about supported tools, clients, models, operating systems, and runtimes.                              |
| Install profiles       | Predefined installation targets for tools such as Copilot, Claude Code, Cursor, Codex, Gemini, Windsurf, or Kiro. |

---

# 8. App and developer surfaces

App surfaces describe where humans inspect, approve, and interact with agentic work.

| Surface                           | Meaning                                                                                                         |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| MCP-enabled app surfaces          | App-like interfaces where MCP tools expose structured resources or UI metadata.                                 |
| External app connectors           | Agent-facing integrations with SaaS tools, calendars, mail, issue trackers, databases, and developer platforms. |
| Embedded widgets                  | Interactive UI components shown inside an AI client.                                                            |
| Deep links and app handoffs       | Moving users from chat or IDE into another app with context preserved.                                          |
| Desktop extensions                | Installable bundles for local agent capabilities or MCP servers.                                                |
| IDE integrations                  | Editor surfaces where agents read code, edit files, run commands, and ask for approval.                         |
| Pull request interfaces           | Review surfaces where agents summarize changes, explain diffs, run checks, and attach evidence.                 |
| Issue tracker integrations        | Surfaces where agents triage issues, clarify requirements, open branches, and produce pull requests.            |
| ChatOps interfaces                | Slack, Teams, Discord, or similar channels for triggering agents and approving work.                            |
| Browser and computer-use surfaces | Environments where agents operate user interfaces directly.                                                     |
| Notification surfaces             | Channels for completed work, blocked tasks, approvals, failing checks, budget alerts, or security events.       |
| Review dashboards                 | Dashboards for agent runs, traces, artifacts, cost, risk, confidence, and approvals.                            |
| Agent session views               | Live views of agent state, plans, actions, tool calls, logs, and approvals.                                     |
| Workspace canvases                | Visual spaces for inspecting generated files, diagrams, notes, plans, and code changes.                         |
| Diff viewers                      | Interfaces for inspecting agent-generated patches.                                                              |
| Trace viewers                     | Interfaces showing how prompts, tool calls, model calls, and subagent work produced an output.                  |
| Approval panels                   | UI components for allowing, denying, modifying, or escalating agent actions.                                    |
| Task boards                       | Project management surfaces where agents pick up tasks, update status, and request review.                      |
| Incident interfaces               | Surfaces where agents investigate alerts, summarize logs, and recommend fixes.                                  |
| Documentation interfaces          | Surfaces where agents generate, edit, review, and maintain documentation.                                       |

---

# 9. Execution and orchestration patterns

Execution patterns describe how agent work is split, delegated, verified, repaired, and merged.

## 9.1 Routing and decomposition

| Pattern               | Meaning                                                                        |
| --------------------- | ------------------------------------------------------------------------------ |
| Classify and act      | Classify the request first, then send it to the right agent or workflow.       |
| Planner-executor      | One agent plans while another executes.                                        |
| Researcher-writer     | One agent gathers context while another produces the final output.             |
| Subagents and routing | A coordinator delegates specialized work to focused agents.                    |
| Dynamic subagents     | An agent programmatically creates or dispatches subagents.                     |
| Tree of agents        | Parent agents split work into subtasks handled by child agents.                |
| Swarm pattern         | Multiple agents collaborate through shared state without one fixed controller. |

## 9.2 Parallelization and search

| Pattern                                       | Meaning                                                                    |
| --------------------------------------------- | -------------------------------------------------------------------------- |
| Fanout and synthesize                         | Run the same operation across many items, then merge the results.          |
| Parallel agents                               | Multiple agents work on separate tasks or solution paths at the same time. |
| Generate and filter                           | Generate several options, then score or filter them.                       |
| Tournament                                    | Compare candidates head-to-head until one remains.                         |
| Explore-exploit                               | Explore several solutions first, then focus on the best one.               |
| Branch and compare                            | Produce alternative patches or branches and compare them.                  |
| Agentic Git branching / speculative execution | Let agents explore competing solutions in isolated branches or worktrees.  |

## 9.3 Verification and repair

| Pattern                      | Meaning                                                                     |
| ---------------------------- | --------------------------------------------------------------------------- |
| Adversarial verification     | One agent produces findings while independent agents verify them.           |
| Evaluator-optimizer loop     | One agent generates, another evaluates, then the first improves the result. |
| Reflection / self-correction | The agent critiques its own work and retries.                               |
| Critic-reviewer              | A separate agent reviews code, docs, or plans.                              |
| Repair loop                  | Feed failing tests, linter errors, or review comments back to the agent.    |
| Two-pass review              | First pass finds possible issues, second pass confirms or rejects them.     |
| Loop until done              | Keep scanning, fixing, or verifying until no new issues appear.             |

## 9.4 Control and safety

| Pattern                 | Meaning                                                                         |
| ----------------------- | ------------------------------------------------------------------------------- |
| Human-in-the-loop gates | Pause before sensitive actions and ask for human approval.                      |
| Plan then act           | Require a plan before tool calls or edits.                                      |
| Act then explain        | Make a bounded change, then explain the diff, tests, risks, and remaining work. |
| Shadow execution        | Simulate or propose actions without applying them.                              |
| Canary agent            | Test a new agent workflow on low-risk tasks before wider use.                   |
| Rollback and recovery   | Make agent actions reversible or replayable.                                    |

## 9.5 Scaling and context control

| Pattern                  | Meaning                                                                         |
| ------------------------ | ------------------------------------------------------------------------------- |
| Map-reduce agent pattern | Many agents inspect separate items, then an aggregator merges findings.         |
| Batch processing         | Process a known list of files, issues, logs, or services with clear coverage.   |
| Progressive widening     | Start with narrow context and expand only when needed.                          |
| Least-context pattern    | Give the agent only what it needs for the current step.                         |
| Context refresh          | Periodically re-read source files or tool outputs to avoid stale assumptions.   |
| Checkpoint and resume    | Save work at safe points so it can continue later.                              |
| Long-running agent       | Let an agent persist across time and resume from checkpoints.                   |
| Event-driven agent       | Trigger agents from events such as issues, CI failures, incidents, or webhooks. |
| Consensus and debate     | Multiple agents propose, critique, vote, or reconcile solutions.                |

---

# 10. Observability and telemetry

Observability helps teams see what the agent actually did.

| Concept                                | Meaning                                                                                             |
| -------------------------------------- | --------------------------------------------------------------------------------------------------- |
| Traceability / step tracing            | Record model calls, prompts, tools, handoffs, decisions, outputs, and errors.                       |
| Cost and token management              | Track token usage, model choice, tool calls, retries, latency, and budget.                          |
| Confidence and uncertainty scoring     | Estimate when an output is reliable, needs verification, or should escalate.                        |
| Span-level tool tracing                | Record each tool call, shell command, edit, browser action, MCP request, or API call.               |
| Prompt and completion capture controls | Decide whether prompts, completions, tool arguments, and context are stored or redacted.            |
| Evaluation traces                      | Replayable records connecting prompts, outputs, tool calls, test results, and scores.               |
| Run lineage                            | The chain of prompts, tools, files, commits, tests, approvals, and artifacts behind a change.       |
| Artifact lineage                       | Inputs, model calls, tools, and intermediate outputs that contributed to a final artifact.          |
| Decision logs                          | Records of important agent or human decisions.                                                      |
| Tool-call analytics                    | Metrics about tool usage, failures, latency, cost, and risk.                                        |
| Model-call analytics                   | Metrics about model usage, latency, tokens, errors, fallbacks, retries, and cost.                   |
| Agent performance dashboards           | Views of task success, failures, verification pass rates, cost, latency, and quality trends.        |
| Drift detection                        | Detect when specs, prompts, skills, dependencies, tools, or architecture no longer match reality.   |
| Audit trails                           | Append-only records of actions, approvals, access decisions, tool calls, artifacts, and policies.   |
| Prompt observability                   | Visibility into which prompts, instructions, context files, and skills were active.                 |
| Context observability                  | Visibility into which files, docs, tickets, or retrieved chunks were used.                          |
| Subagent observability                 | Visibility into delegated work and subagent outputs.                                                |
| Approval observability                 | Visibility into who approved what, what evidence they saw, and what changed afterward.              |
| Risk observability                     | Visibility into risky actions, sensitive data exposure, policy violations, and blocked tool calls.  |
| Repository-level agent analytics       | Metrics by repository, branch, pull request, issue, team, or workflow.                              |
| Pull request agent traces              | Traces that connect AI activity to a pull request, branch, commit, or diff.                         |
| Token budget alerts                    | Alerts when usage approaches cost or token limits.                                                  |
| Latency monitoring                     | Tracking model latency, tool latency, workflow runtime, queue time, and approval delay.             |
| Error classification                   | Grouping failures as tool error, model error, permission error, test failure, timeout, and similar. |
| Telemetry redaction                    | Masking secrets, personal data, proprietary code, prompts, completions, or tool arguments.          |
| Sampling controls                      | Deciding which traces or outputs are kept, sampled, summarized, or dropped.                         |

---

# 11. Evaluation and benchmarking

Evaluation helps teams check whether agents are useful, correct, safe, and improving.

| Concept                | Meaning                                                                                               |
| ---------------------- | ----------------------------------------------------------------------------------------------------- |
| Task-level evals       | Check whether an agent completed a specific task correctly.                                           |
| Repository-level evals | Test whether an agent can work inside a real codebase while preserving behavior.                      |
| Regression evals       | Detect whether a new model, prompt, skill, tool, or workflow performs worse than before.              |
| Golden task sets       | Curated internal tasks with known expected outcomes and verification commands.                        |
| SWE-bench-style evals  | Benchmarks where agents resolve real or realistic software engineering issues through patches.        |
| Tool-use evals         | Measure whether agents choose the right tools and use them safely.                                    |
| Security evals         | Test prompt injection, unsafe code, privilege abuse, secret exposure, and policy bypass.              |
| Human preference evals | Humans compare outputs for usefulness, maintainability, readability, and risk.                        |
| LLM-as-judge evals     | Another model scores outputs, traces, plans, or diffs against a rubric.                               |
| Execution-based evals  | Run generated code, tests, commands, or workflows instead of only judging text.                       |
| Trace-based evals      | Inspect the steps, tool calls, evidence, and approvals behind the final output.                       |
| Cost-quality evals     | Compare task success against tokens, latency, cost, retries, and human review effort.                 |
| A/B agent testing      | Compare agent versions, prompts, models, tools, or policies on similar tasks.                         |
| Prompt evals           | Compare prompt templates, instructions, or context files.                                             |
| Skill evals            | Test whether skills trigger correctly and improve outcomes.                                           |
| Agent profile evals    | Compare specialist agents, roles, instructions, and tool scopes.                                      |
| Workflow evals         | Test full workflows including planning, tool use, delegation, verification, and review.               |
| Guardrail evals        | Check whether filters, policy checks, and approval gates fire when they should.                       |
| Dataset-backed evals   | Run workflows against curated examples, logs, issues, support tickets, or incidents.                  |
| Synthetic evals        | Generate artificial cases for edge cases, attacks, rare states, or scale.                             |
| Live evals             | Evaluate real or near-production agent traffic with safeguards.                                       |
| Offline evals          | Evaluate stored traces, tasks, prompts, diffs, or artifacts.                                          |
| Canary evals           | Test new models, tools, prompts, or policies at small scale first.                                    |
| Red-team evals         | Adversarial tests designed to break assumptions or bypass guardrails.                                 |
| Business outcome evals | Connect agent behavior to cycle time, review quality, incidents, defects, or documentation freshness. |

---

# 12. Security and governance

Security and governance keep agentic work controlled, reviewable, and auditable.

| Concept                                 | Meaning                                                                                                     |
| --------------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Input / output guardrails               | Validate prompts, context, outputs, code, tool arguments, and downstream actions.                           |
| Agentic access control / IAM for agents | Treat agents as risk-scoped actors with identity, permissions, and audit logs.                              |
| Compliance and policy engines           | Evaluate agent actions against rules, evidence requirements, data boundaries, and approvals.                |
| Least-privilege tool access             | Give agents only the tools, data, credentials, and filesystem access they need.                             |
| Scoped credentials                      | Use short-lived, purpose-limited credentials for specific actions or sessions.                              |
| Prompt injection defenses               | Detect or isolate malicious instructions in user input, docs, websites, issues, logs, or tool outputs.      |
| Context sanitization                    | Filter, redact, classify, and trust-label context before giving it to an agent.                             |
| Secret detection                        | Prevent agents from reading, exposing, copying, or committing credentials.                                  |
| Data loss prevention (DLP)              | Block sensitive data from being sent to models, tools, logs, traces, or third parties.                      |
| Tool risk classification                | Classify tools by risk, such as read-only, write-capable, financial, production-impacting, or irreversible. |
| Action approval policies                | Require approval before high-risk operations.                                                               |
| Policy-as-code                          | Define agent rules in machine-readable policy files.                                                        |
| Runtime isolation                       | Use sandboxes, containers, network limits, filesystem boundaries, and process controls.                     |
| Supply chain scanning                   | Review agent dependencies, skills, prompts, tools, MCP servers, plugins, and packages.                      |
| Audit-ready evidence                    | Record what the agent accessed, changed, generated, verified, and got approved.                             |
| Kill switches                           | Emergency controls to pause, disable, revoke, or quarantine agents and tools.                               |
| Agent identity                          | Give each agent, workflow, or run a unique identity for authorization and audit.                            |
| Delegated authorization                 | Let agents act on behalf of users or services with bounded authority.                                       |
| Just-in-time access                     | Grant access only when needed and revoke it afterward.                                                      |
| Break-glass controls                    | Emergency access paths with stronger logging, review, and expiry.                                           |
| Separation of duties                    | Prevent the same agent from creating, approving, and deploying high-risk changes alone.                     |
| Human approval gates                    | Require a person to approve sensitive actions.                                                              |
| Automated denial gates                  | Automatically block actions that violate policy or exceed risk limits.                                      |
| Sensitive data classification           | Label data, files, prompts, outputs, and traces by sensitivity.                                             |
| Tool output trust levels                | Classify tool outputs by whether they are trusted, external, user-controlled, or untrusted.                 |
| Untrusted context isolation             | Separate untrusted instructions from trusted system, developer, repository, and policy instructions.        |
| Permission diffing                      | Review how a change affects agent permissions, tools, scopes, or access paths.                              |
| Policy simulation                       | Test whether an action would be allowed before attempting it.                                               |
| Continuous compliance monitoring        | Check that agent runs, packages, tools, and workflows remain within policy.                                 |
| Agent inventory                         | Catalog deployed agents, owners, purposes, permissions, dependencies, and risks.                            |
| Agent decommissioning                   | Disable, archive, or delete agents, credentials, prompts, skills, tools, and packages no longer needed.     |

---

# 13. Supply chain and reproducibility

This section covers how teams track and reproduce the context, tools, models, prompts, skills, and runtime dependencies used by agents.

| Concept                       | Meaning                                                                                                                     |
| ----------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| Agent context as dependency   | Treat instructions, skills, prompts, tools, hooks, plugins, and MCP servers as versioned dependencies.                      |
| Version-pinned agent context  | Pin agent dependencies by version, commit, digest, or content hash.                                                         |
| Agent dependency review       | Review changes to prompts, skills, instructions, tools, MCP servers, plugins, and policies.                                 |
| Agent SBOM                    | Inventory agent components such as models, tools, skills, prompts, plugins, servers, and policies.                          |
| Signed agent packages         | Verify package contents, source, publisher, and integrity before use.                                                       |
| Content-hash verification     | Detect whether package contents changed since they were locked, approved, or audited.                                       |
| License and provenance checks | Review licenses, authorship, source repos, dependencies, and trust metadata.                                                |
| Policy-gated installation     | Block or escalate package installs that violate rules or risk thresholds.                                                   |
| Cross-client deployment       | Install the same agent context across tools such as Copilot, Claude Code, Cursor, Codex, Gemini, Windsurf, or Kiro.         |
| Context drift detection       | Detect when deployed agent context differs from the manifest, lockfile, approved version, or repository policy.             |
| CI enforcement                | Validate manifests, lockfiles, hashes, and security policy before merge.                                                    |
| Prompt supply chain           | Track how prompts are authored, reviewed, versioned, packaged, installed, executed, and audited.                            |
| Skill supply chain            | Track how reusable skills are authored, tested, distributed, installed, updated, and retired.                               |
| Tool supply chain             | Track how tools, APIs, MCP servers, and command wrappers are added to an agent runtime.                                     |
| Model supply chain            | Track which models, providers, versions, endpoints, and routing policies were used.                                         |
| Context provenance            | Record where instructions, retrieved context, files, examples, and knowledge came from.                                     |
| Reproducible runs             | Capture inputs, context, tools, model settings, packages, and environment metadata so runs can be replayed or approximated. |
| Environment pinning           | Pin OS images, package versions, tools, runtime settings, and dependency caches.                                            |
| Package attestation           | Signed evidence that a package was built, tested, scanned, and published through an approved process.                       |
| Dependency update automation  | Automatically propose, test, and review updates to agent packages, prompts, skills, tools, and MCP servers.                 |
| Vulnerability management      | Identify, prioritize, patch, and audit vulnerable agent dependencies.                                                       |
| Deprecated package blocking   | Prevent agents from using obsolete, unsafe, abandoned, or policy-blocked packages.                                          |
| Reproducibility reports       | Summaries of which agent context, tools, models, packages, and policies were active for a run.                              |

---

# 14. Packaging

Packaging describes how agent capabilities are bundled, versioned, installed, shared, and reproduced.

| Package type                 | What it contains                                                                                                                                                |
| ---------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Agent Package Manager (apm)  | A package manager for versioning and installing agent context such as skills, prompts, tools, instructions, hooks, plugins, MCP servers, and agent definitions. |
| Agent packages               | Versioned bundles of prompts, skills, instructions, agents, hooks, plugins, and MCP server definitions.                                                         |
| Skill packages               | Portable bundles of instructions, scripts, assets, and references for repeatable capabilities.                                                                  |
| Plugin packages              | Bundles of agents, skills, hooks, MCP servers, settings, and policy modules.                                                                                    |
| Workflow packages            | Reusable workflows with routing logic, tools, evals, guardrails, and approval gates.                                                                            |
| MCP server packages          | MCP server config, runtime commands, auth instructions, exposed tools, and metadata.                                                                            |
| Policy packages              | Access rules, approval requirements, guardrails, audit controls, and compliance checks.                                                                         |
| Evaluation packages          | Eval suites, rubrics, golden tasks, fixtures, and scoring logic.                                                                                                |
| Repository starter kits      | Templates with agent instructions, specs, evals, hooks, CI checks, and governance defaults.                                                                     |
| Organization agent toolkits  | Company-wide engineering standards, architecture rules, security policies, review expectations, and domain knowledge.                                           |
| Prompt packages              | Reusable prompts, prompt files, task templates, and review rubrics.                                                                                             |
| Instruction packages         | Coding conventions, architecture rules, documentation standards, and team preferences.                                                                          |
| Hook packages                | Hook bundles that enforce rules, run checks, validate tool calls, or trigger notifications.                                                                     |
| Connector packages           | Config for GitHub, Jira, Slack, databases, cloud providers, and observability platforms.                                                                        |
| Runtime packages             | Sandbox images, toolchains, setup commands, command allowlists, and execution policies.                                                                         |
| Model configuration packages | Model routing, provider settings, fallback rules, temperature defaults, context limits, and budgets.                                                            |
| Team packages                | Skills, prompts, tools, instructions, hooks, policies, and evals for a specific team.                                                                           |
| Project packages             | Repository-specific architecture, commands, test rules, dependency boundaries, and delivery workflows.                                                          |
| Security packages            | Secret scanning, prompt injection checks, policy gates, access controls, and audit requirements.                                                                |
| Compliance packages          | Policy and evidence bundles for regulated engineering workflows.                                                                                                |
| Documentation packages       | Instructions, templates, and workflows for generating and maintaining documentation.                                                                            |
| Review packages              | Code review instructions, checklists, scoring rubrics, and pull request comment patterns.                                                                       |
| Release packages             | Changelogs, version bumps, release notes, deployment checks, and rollout plans.                                                                                 |

---

# Source anchors

This guide combines established standards, documented tools, emerging conventions, and useful engineering patterns.

Useful source anchors include:

* Model Context Protocol (MCP)
* Agent2Agent Protocol (A2A)
* Agent Client Protocol (ACP)
* Agent User Interaction Protocol (AG-UI)
* GitHub Spec Kit
* OpenAI Codex
* Claude Code
* GitHub Copilot custom agents
* OpenHands
* SWE-agent
* SWE-bench
* OpenTelemetry GenAI semantic conventions
* OpenInference
* SARIF
* CycloneDX
* SPDX
* Microsoft Agent Package Manager (apm)

# Contributing

Contributions are welcome.

Good additions should include:

* A clear name
* A short explanation
* A source when the item is a standard, protocol, product, framework, or benchmark
* A reason why the concept belongs in agentic software engineering
