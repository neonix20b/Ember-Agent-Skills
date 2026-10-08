# Help a contributor add a board

Use this when a developer wants to bring another board to EmberBSD, adapt an
existing platform, or publish board validation. These instructions are for
users of the installed skill, not permissions for the EmberBSD maintainers' lab.

Start with the current [board catalog](https://github.com/oxtech-ember/EmberBSD/tree/main/ember/boards)
and [board contribution guide](https://github.com/oxtech-ember/EmberBSD/blob/main/ember/boards/adding-a-board.md).
Read those files in the chosen OS checkout too. The OS owns the board procedure,
source layout, build commands and support evidence; do not maintain an alternative
driver recipe inside this skill.

## Establish the target

Identify the model and revision, SoC/architecture, RAM, boot media, serial
console, firmware chain, and whether the platform exposes device tree or ACPI.
Use public vendor schematics/manuals and inspect actual EmberBSD/NetBSD sources.
Identify what differs from the closest working board: pin wiring, PHY, storage,
power management, radio firmware and boot selection often differ within one SoC.

Ask for missing facts that block the requested bring-up, such as access to the
target board or its serial log. Continue independent source/build work when it
can make progress, and label it at that level. Do not infer physical support from
a similar board, an upstream driver, a compile, or a QEMU boot.

## Make the contribution complete

Keep kernel, DTS/ACPI, boot and build integration in the OS repository. Reuse
its actual builders and source contracts. Adding a DTS alone may not include
that DTB in the output or make the loader choose it; inspect both paths.
Adaptations already applied to the fork must not be applied a second time.
Preserve existing bindings, ABIs, provenance and licenses.

Use Ports for third-party dependencies and Examples for a reusable application
demonstration. A board contribution does not require a new Runtime/SDK interface
or an application agent. Never copy private credentials or personalized images
into any public contribution.

Build the relevant kernel/configuration, modules, device tree and firmware from
recorded inputs. Keep their output hashes and avoid mixing revisions. Identify
the artifact actually selected by the loader: a QEMU host's direct `-kernel`
input may differ from the guest's `/netbsd`. Test the
changed common paths on a known configuration when applicable. Follow the
contributor's task scope for flashing/reboots, and identify a physical target
before writing it. Skill installation alone does not authorize device changes.

## Describe and publish the evidence

Use one board page with a two-column capability table and a short catalog/README
entry, following the OS guide. Include the model/revision, test date, OS commit,
configuration, firmware, toolchain, scenario, duration, measurements and known
limits. Keep build-only or VM-only results explicit. Missing historical metadata
stays unknown; copying an older table is not a new test.

Prefer useful end-to-end checks: checked storage transfers, bidirectional network
data, an actual watchdog reset, or captured/played audio. Controller attachment
and device discovery are intermediate results. Record failed and untested cases,
and update claims after a regression as well as after a successful test.

When contribution publication is authorized, follow
[the contribution workflow](contributions.md): a focused branch/fork, relevant
tests, and a PR against the correct repository/base. Include code, build paths,
regressions and board documentation together. State the gaps and use a draft
where permitted if required hardware validation is unavailable. Do not auto-merge
or transfer maintainer permissions to an external contributor.

Update this reference only when a verified result changes reusable guidance.
Keep board-specific facts and workarounds with the board's source documentation.
