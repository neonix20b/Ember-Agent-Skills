# Tested contributions to EmberBSD and upstream

Use this for a completed fix, new port, or reusable compatibility adaptation.
The workflow applies to both EmberBSD repositories and the original upstream.
Task-specific user instructions and the accepting project's current rules take
precedence over a remembered branch or submission convention.

## Before opening a PR

1. Reproduce the issue or establish the requested behavior. Identify the owning
   component and check for an existing fix, issue or PR before duplicating it.
2. Read the target's current CONTRIBUTING/AGENTS guidance, supported branches,
   required tests, patch format, licensing and AI-assistance policy. Verify that
   the repository accepts PRs rather than assuming its GitHub mirror does.
3. Implement the smallest complete change. Keep fixes, tests and necessary user
   instructions together; split independent changes into separate contributions.
4. Run relevant tests on the exact proposed revision. For a bug fix, show the
   regression failing before and passing after. For a port, demonstrate build,
   package installation and a useful runtime scenario, with untested targets
   stated explicitly. A documentation change needs link and instruction checks,
   not an unrelated full OS build.
5. Recheck the diff for unrelated files, generated binaries and private data.
   Preserve upstream authorship and disclose AI assistance accurately.
6. Open the tested contribution against the correct branch. Prefer updating an
   existing related PR over creating a duplicate. Follow branch protection and
   do not force-push, overwrite another developer's work or merge automatically.

A genuine failing test remains a failure. Diagnose and fix it before presenting
the contribution as ready. If required validation is unavailable, state the
precise gap; only submit a draft when the task and target workflow permit it.
A reproduced bug without a fix can justify an issue through the target's normal
channel; do not create an empty PR to satisfy this rule.

## Put the change in the right place

An EmberBSD PR carries the recipe or fix needed by the project. A reusable
upstream PR carries the minimal change against the original project's current
accepted base, without EmberBSD-only packaging or unrelated adaptations.
Test that rebased upstream change separately and cross-link both submissions.
One passing downstream build does not establish upstream acceptance.

If the project uses a mailing list, patch queue or problem report, use that
documented channel instead of a PR to a mirror. Check task authorization before
messages to new external recipients. Keep a prepared patch and report an exact
permission or policy block rather than silently skipping the contribution.

For example, the [pkgsrc submission guide](https://www.netbsd.org/docs/pkgsrc/submit.html)
describes pkgsrc-wip, pkglint and a `pkg` problem report. The
[NetBSD commit rules](https://www.netbsd.org/developers/commit-guidelines.html)
require prior written core approval for committing LLM-generated code. Checked
2026-10-06: re-read the applicable policy before submission. Do not conceal AI
origin or treat tests as a substitute for required upstream approval.

## Write a useful description

Lead with the concrete problem and the resulting behavior. Explain why the
change belongs here, how to reproduce it, what was tested, and what remains
unverified. Follow the repository's own template; the following is a fallback:

```markdown
## Problem and change
Concrete trigger, previous behavior, and resulting behavior.

## Reproduce and validate
- Source/base and tested commit:
- OS, architecture, toolchain and relevant dependency versions:
- Commands and actual results (including before/after regression):
- Runtime/hardware limits and skipped tests:

## Provenance and maintenance
Original source/release and hashes for a port; patch authorship and license.
AI assistance, upstream issue/PR links, and workaround removal condition.
```

Scale the description to the change; do not add irrelevant empty sections.
Record the returned URL and actual state: prepared, submitted, reviewed, merged,
or released. These states are not interchangeable. Handle review findings with
focused fixes and relevant checks, then update the same PR and instructions.
