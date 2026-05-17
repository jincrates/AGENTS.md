# AGENTS.md

Problem definition → small, safe change → change review → refactor — repeat the loop.

## Mandatory Rules

- Before changing anything, read the relevant files end to end, including all call/reference paths.
- Keep tasks, commits, and PRs small.
- If you make assumptions, record them in the Issue/PR/ADR.
- Never commit or log secrets; validate all inputs and encode/normalize outputs.
- Avoid premature abstraction and use intention-revealing names.
- Compare at least two options before deciding.

## Mindset

- Think like a senior engineer.
- Don’t jump in on guesses or rush to conclusions.
- Always evaluate multiple approaches; write one line each for pros/cons/risks, then choose the simplest solution.

## Code & File Reference Rules

- Read files thoroughly from start to finish (no partial reads).
- Before changing code, locate and read definitions, references, call sites, related tests, docs/config/flags.
- Do not change code without having read the entire file.
- Before modifying a symbol, run a global search to understand pre/postconditions and leave a 1–3 line impact note.

## Required Coding Rules

- Before coding, write a Problem 1-Pager: Context / Problem / Goal / Non-Goals / Constraints.
- Enforce limits: file ≤ 300 LOC, function ≤ 50 LOC, parameters ≤ 5, cyclomatic complexity ≤ 10. If exceeded, split/refactor.
- Prefer explicit code; no hidden “magic.”
- Follow DRY, but avoid premature abstraction.
- Isolate side effects (I/O, network, global state) at the boundary layer.
- Catch only specific exceptions and present clear user-facing messages.
- Use structured logging and do not log sensitive data (propagate request/correlation IDs when possible).
- Account for time zones and DST.

## Testing Rules

- New code requires new tests; bug fixes must include a regression test (write it to fail first).
- Tests must be deterministic and independent; replace external systems with fakes/contract tests.
- When adding or changing e2e coverage, include ≥1 happy path and ≥1 failure path.
- For docs/config-only changes, explain why runtime tests are not needed.
- Proactively assess risks from concurrency/locks/retries (duplication, deadlocks, etc.).

## Commit Rules

- Commit titles must use a Conventional Commit type prefix such as `feat:`, `fix:`, `docs:`, `test:`, `refactor:`, `build:`, `ci:`, or `chore:`.
- After the Conventional Commit prefix, write the commit title in Korean by default unless the user explicitly requests another language.
- Do not create, amend, or push commits unless the user explicitly asks.
- Commit bodies should list what changed as plain bullet points before the trailer.
- Keep commit body bullet items contiguous, with no blank lines between bullet items.
- For multi-line commit bodies, use a commit message file or a single body argument that preserves adjacent bullet lines; do not pass each bullet as a separate `-m` paragraph.
- When Codex creates or amends a commit, include a `Co-Authored-By` trailer by default.
- Use the requested or active model name when it is explicitly available, for example `Co-Authored-By: GPT 5.5 <codex@openai.com>`.
- If the requested or active model name is not visible, use `Co-Authored-By: Codex <codex@openai.com>` rather than guessing a model version.
- Omit the trailer only when explicitly requested.

## Security Rules

- Never leave secrets in code/logs/tickets.
- Validate, normalize, and encode inputs; use parameterized operations.
- Apply the Principle of Least Privilege.

## Clean Code Rules

- Use intention-revealing names.
- Each function should do one thing.
- Keep side effects at the boundary.
- Prefer guard clauses first.
- Symbolize constants (no hardcoding).
- Structure code as Input → Process → Return.
- Report failures with specific errors/messages.
- Make tests serve as usage examples; include boundary and failure cases.

## Anti-Pattern Rules

- Don’t modify code without reading the whole context.
- Don’t expose secrets.
- Don’t ignore failures or warnings.
- Don’t introduce unjustified optimization or abstraction.
- Don’t overuse broad exceptions.
