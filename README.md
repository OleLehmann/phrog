# 🐸 Phrog

### The autonomous AI agent for PHP.

**It doesn't just write PHP. It tests, debugs, fixes, and verifies it.**

Phrog is an AI-powered coding agent designed to work directly inside PHP codebases. Give it a task, a bug report, or a failing test, and Phrog explores the repository, plans a solution, modifies the necessary files, runs verification tools, and iterates on its changes.

From legacy PHP applications to modern Laravel backends, Phrog is built to turn natural-language instructions into working, verifiable code.

```text
   PHROG // AUTONOMOUS PHP ENGINE

   [ TASK RECEIVED ]
          |
          v
   [ EXPLORE THE SWAMP ]
          |
          v
   [ UNDERSTAND THE CODE ]
          |
          v
   [ PLAN THE CHANGES ]
          |
          v
   [ WRITE PHP ]
          |
          v
   [ RUN TESTS & LINT ]
          |
          v
      Tests pass?
       /       \
     YES        NO
      |          |
      v          v
   [ VERIFY ] [ DEBUG & RETRY ]
      |
      v
   [ PRESENT DIFF ]
```

## 🐸 Why Phrog?

Most coding assistants can generate code. Phrog is designed to close the loop between generating code and verifying that it works.

Instead of producing a snippet and leaving the developer to figure out the rest, Phrog works through a structured agent workflow: inspect, reason, implement, execute, evaluate, and improve.

### Core capabilities

- **Codebase Intelligence** — Explore repositories, trace dependencies, understand application structure, and identify relevant files before making changes.
- **Autonomous Code Editing** — Implement features, fix bugs, refactor functions, and modify existing PHP applications.
- **Self-Verification Loop** — Run syntax checks, test suites, static analysis, and other available project checks after editing.
- **Iterative Debugging** — Analyze errors from failed checks, make targeted corrections, and retry within a configurable budget.
- **PHP Security Analysis** — Detect potentially unsafe queries, authorization mistakes, insecure deserialization, unsafe file handling, and exposed secrets.
- **Framework Awareness** — Work with Laravel, Symfony, Composer-based projects, and traditional PHP applications.
- **Human-in-the-Loop Control** — Review diffs, approve sensitive operations, and maintain control over consequential changes.

## 🧠 The Phrog Agent

Phrog is organized around a tool-using AI agent with a verification-oriented execution cycle.

### 1. Swamp Scanner

Before changing code, Phrog investigates its environment.

It can inspect:

- Project files and directory structure
- `composer.json` and dependency configuration
- Routes, controllers, models, and middleware
- Existing tests and application entry points
- PHP version requirements and framework conventions
- Git status and existing uncommitted changes

The objective is to understand the project before touching it.

### 2. Task Planner

Phrog converts a natural-language request into an actionable plan.

Example:

> Add rate limiting to the public API endpoints and write tests for the new behavior.

The agent identifies the relevant middleware, routes, configuration, and test files before implementing the changes.

### 3. Code Execution Engine

Phrog uses controlled tools to read files, edit code, execute permitted commands, and inspect their output.

It can be designed to support:

- PHP file editing
- Shell commands
- PHPUnit tests
- PHP syntax validation
- PHPStan or Psalm static analysis
- Composer scripts
- Framework-specific test commands

Available checks depend on the project's installed dependencies and configuration.

### 4. The Ribbit Loop

The Ribbit Loop is Phrog's defining feature.

After making a change, the agent evaluates the result instead of assuming the implementation is correct.

```text
IMPLEMENT
    |
    v
EXECUTE CHECKS
    |
    v
COLLECT ERRORS
    |
    v
ANALYZE FAILURE
    |
    v
PATCH THE PROBLEM
    |
    +------> RETRY WITHIN BUDGET
    |
    v
VERIFY OR REPORT BLOCKER
```

The loop terminates when the configured checks pass, the retry budget is exhausted, or the agent requires human intervention.

Phrog should report exactly which checks ran, which passed, which failed, and which were skipped.

### 5. Predator Mode

PHP applications often contain security-sensitive logic. Predator Mode focuses on reviewing it.

Potential checks include:

- SQL injection and unsafe query construction
- Missing authentication or authorization checks
- Insecure deserialization
- Unsafe file uploads and path traversal
- Cross-site scripting and unsafe output rendering
- Hardcoded credentials and exposed secrets
- Dangerous command execution
- Missing input validation

Findings should include the affected file, relevant code location, severity, explanation, and suggested remediation.

Static analysis and AI-generated findings are signals for review, not guarantees that a vulnerability exists or that an application is secure.

## 🛠️ Architecture

Phrog can be built as a modular agent with five main components.

| Component | Responsibility |
|---|---|
| Agent Core | Interprets tasks and coordinates the workflow |
| Repository Explorer | Reads project files and builds code context |
| Tool Runtime | Executes approved commands and applies edits |
| Verification Engine | Runs tests, linting, and static analysis |
| Safety Layer | Enforces permissions, limits, and approval policies |

The model provider should be configurable so the agent can evolve independently of its execution environment.

## 🚀 Example Workflow

Imagine inheriting a legacy PHP application with a broken registration endpoint.

You run:

```bash
phrog "Fix the registration endpoint and add regression tests"
```

Phrog's intended workflow:

1. Inspect the registration route and its dependencies.
2. Trace the controller, validation logic, and persistence layer.
3. Identify the likely source of the failure.
4. Implement a targeted fix.
5. Add or update regression tests.
6. Run PHP syntax checks and the relevant test suite.
7. Investigate failures and retry within the configured budget.
8. Present a final summary and Git diff.

The result is not simply generated code. It is a proposed code change accompanied by evidence from the checks that actually ran.

## 💻 CLI Experience

The command-line interface is the primary interface for Phrog.

```bash
# Investigate a codebase
phrog analyze .

# Find and explain a bug
phrog "Find why password reset emails are failing"

# Implement a feature
phrog "Add pagination to the users API"

# Fix a failing test
phrog fix --tests

# Review potential security issues
phrog security .

# Run the verification workflow
phrog verify .
```

These commands describe the intended interface; each command requires implementation before it can be used.

## 🔒 Safety First

An autonomous coding agent needs boundaries.

Phrog should be designed with the following safeguards:

- **Diff-first review:** Show the proposed changes before accepting them.
- **Permissioned execution:** Restrict commands and filesystem access to an explicit policy.
- **Protected operations:** Require approval for destructive actions, deployments, and other high-impact operations.
- **Secret protection:** Avoid exposing credentials in prompts, logs, and generated reports.
- **Retry budgets:** Bound execution time, tool calls, and repair attempts.
- **Git awareness:** Preserve unrelated work and detect pre-existing modifications.
- **Honest verification:** Never claim a test passed unless it actually executed successfully.

AI-generated code should be treated as untrusted until reviewed and validated.

## 🗺️ Roadmap

- [ ] PHP-aware repository explorer
- [ ] Agent core and tool-calling runtime
- [ ] Safe file editing and diff generation
- [ ] CLI task interface
- [ ] PHP syntax validation
- [ ] PHPUnit integration
- [ ] Ribbit Loop with bounded retries
- [ ] Laravel and Symfony project awareness
- [ ] PHPStan and Psalm integration
- [ ] Security review mode
- [ ] Configurable model providers
- [ ] Interactive approval workflow
- [ ] Structured run reports and reproducible evaluations

## 🎯 Design Philosophy

**Understand before editing. Verify before finishing.**

Phrog should optimize for useful changes, reproducible checks, transparent reasoning summaries, and developer control—not for the number of files it can modify or the number of tokens it can generate.

An agent that knows when to stop, report a blocker, or ask for approval is more useful than one that blindly keeps editing.

## 🐸 The Mission

PHP powers an enormous amount of the web, including applications that have evolved over years of patches, dependencies, and changing requirements.

Phrog aims to make working with those applications less tedious by bringing autonomous investigation, implementation, and verification into one focused development agent.

**Less debugging by hand. More verified PHP.**

*Ribbit. Ship it only when it's checked.*
