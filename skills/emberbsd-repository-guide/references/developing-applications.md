# Build an application with EmberBSD

This guide is for people using EmberBSD and their coding assistants. Work in
the user's application repository; consult EmberBSD sources when the task needs
them. Installing this skill does not make an application an EmberBSD project or
give its assistant maintainer access to EmberBSD repositories.

## Establish a usable starting point

Read the application's own instructions. Identify its purpose, target board or
VM, OS image/revision, architecture, dependencies and available test environment
from the checkout and user context. Ask only for missing facts that affect the
implementation. Keep the user's language, licensing and publication choices.
English and no-new-Python rules apply to contributions to EmberBSD repositories;
they do not impose a language or license on independently owned applications.

Use the [repository map](repositories.md) to find the relevant public example,
package or interface. Clone only what is needed. Prefer a working example's
documented dependencies and build path over rebuilding the OS for an application
change. Verify compatibility with the user's target and retain attribution when
adapting example code. A library may need a Ports adaptation first.

Inspect actual SDK/Runtime releases or sources before using their APIs. A planned
Wasm package format, marketplace, command or hardware adapter is not a usable
interface. When the required component is absent, explain that limitation and
use an existing supported path if it satisfies the user's task.

## Give the next developer a reproducible result

Keep build and runtime instructions beside the application. A useful README
answers these questions with tested commands and explicit parameters:

- What does the program do, and on which environment was it checked?
- Which compiler, dependencies and configuration are required?
- How do I build it from a clean checkout and run its tests?
- How do I run the smallest demonstration, and what result should I see?
- Which capabilities need real hardware, and what has not been verified?

Use public inputs or synthetic fixtures for published examples. Explain device
paths and configuration with replaceable values; never rely on the author's
private files, accounts or network. Mark commands as host or target commands
when that distinction matters. Include a meaningful failure path, such as a
missing device or malformed input, when relevant to the program.

Compile and test against the selected target. A test on the development host
does not prove EmberBSD execution; a VM does not prove the user's board. Record
the actual environment and results. Deploy, reboot or flash only when that work
is part of the task, using an identified device and a recovery path.

## Return reusable improvements to the ecosystem

Keep application-specific code in the user's project. When a task uncovers a
reusable EmberBSD defect, missing port or incorrect instruction, isolate that
change in its owning repository. Reproduce and fix it, add relevant checks, and
include the instructions another developer needs to use the result.

For an authorized contribution, finish with a tested PR using the
[contribution workflow](contributions.md). Public fixes and ports belong on a
contribution branch, normally in the contributor's fork; installing the skill
does not grant permission to push to an upstream default branch. Offer reusable
patches to the original upstream through its accepted process too.

If publication is outside the user's task or involves private application
material, prepare the minimal reviewable patch and seek publication permission
before sending it. A private application does not need to become public to use
EmberBSD. Report an unfixed reproducible defect through an authorized issue or
problem-report workflow; do not open an empty PR.

Update the relevant [maintained guidance](maintenance.md) when a tested result
changes a reusable rule. The application README, port recipe and assistant skill
serve different readers; link to the source of truth instead of copying it.
