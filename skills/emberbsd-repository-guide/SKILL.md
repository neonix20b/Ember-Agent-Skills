---
name: emberbsd-repository-guide
description: "Route EmberBSD development tasks to the owning repository and establish the available interfaces and validation evidence. Use when starting EmberBSD work, deciding between OS, Examples, Runtime, SDK, or Agent-Skills changes, or assessing a claimed EmberBSD capability."
---

# EmberBSD repository guide

Establish where a change belongs and what the current sources actually support.
Use this guide before selecting an EmberBSD build command, API, or example.

## Locate the owner

Read [the repository map](references/repositories.md). Respect an explicitly
selected repository, and explain any dependency that belongs elsewhere.

Find an existing checkout before cloning. Inspect its remote, branch, revision,
and uncommitted changes. Read its applicable `AGENTS.md`, README, and documentation
for the requested subsystem. Preserve unrelated work.

Do not assume these skill files live in the user's working repository. Resolve
bundled references relative to this `SKILL.md`; resolve project paths against the
identified checkout.

## Establish the supported workflow

1. Find the actual API definitions, build commands, examples, and tests in that
   checkout. Cite their paths and the inspected revision when reporting support.
2. Treat the repository map as intended ownership. A named repository does not
   establish that its planned component has been implemented or released.
3. If the SDK or Runtime lacks the required interface, report that gap and work
   from available sources. Do not invent commands, imports, package formats,
   hardware MCP tools, or compatible version ranges.
4. For cross-repository changes, identify the shared contract and its owner.
   Keep ABI definitions and build tools with their owning project; call them
   from skills instead of maintaining alternative implementations here.

## Make and validate the change

Follow the target project's conventions and task authorization. Use English in
public source, documentation, comments, and commit messages. Preserve upstream
licenses and attribution. Use NetBSD KNF for C where required by the target.
New EmberBSD utilities, tests, and examples must not introduce Python; account
honestly for existing upstream dependencies.

Choose checks that demonstrate the requested behavior. Distinguish inspected
source, a successful build, contract tests, a VM boot, and a physical board test.
For hardware claims, record the board, firmware, configuration, test conditions,
and unverified components. Compilation alone does not establish device support.

Use the user's authorized scope for commits, publication, and deployment.
A request to write an application does not by itself request flashing a board.
Public examples and reports must work without private configuration or secrets.

Report the owning repository, changes or findings, checks actually run, and
remaining gaps. If a required checkout or tool is unavailable, state the exact
limitation rather than implying that validation passed.
