# Keep guidance useful and current

Update guidance as part of the work that changes it: a verified port, confirmed
failure mode, changed build command, upstream acceptance, or retired workaround.
This is an event-driven maintenance rule; it does not claim that an unattended
monitor is running or authorize unrelated scheduled work.

Keep reusable decisions in this skill. Keep source-level recipes, executable
checks and detailed recovery instructions in the owning public repository.
Link them instead of maintaining a second implementation or copying full logs.
Never require a private wiki, local machine path, credential or personal image
to use a published skill.

For each non-obvious workaround or compatibility case, preserve:

- the symptom and cause, distinguishing confirmed cause from a hypothesis;
- affected platform and version range, plus the source URL and checked revision;
- the smallest verified remedy and the command or regression that demonstrates it;
- known limits, upstream submission status and the condition that removes it.

Recheck unstable facts before using them. When upstream fixes the problem,
verify the new version, remove the local patch if appropriate, and replace the
old instruction. A removed workaround should not survive as a blanket ban.
Do not add rules based only on a single unexplained failure.

Before publishing a guidance update, inspect its links and run the package check
documented in the root README. Run native Codex discovery when available and
record the CLI version. For behavior changes, exercise a realistic relevant
scenario using only resources and side effects authorized for that check.
Discovery validates packaging; it does not demonstrate successful porting.

Update the package version, README use cases and installation/refresh guidance
when they change. Explain prerequisites, a copyable command, expected output,
and recovery or limits where relevant. Mark other IDE integrations unverified
until tested; portable Markdown alone does not prove client compatibility.
