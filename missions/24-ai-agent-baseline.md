# Mission: Use A Safe Agent Loop After The Manual Baseline

## Outcome

Decide what an agent may change, reject an extra action, and verify its actual
work before accepting it.

## Concept

An AI coding agent can read files and propose edits or commands. An ordinary
chat window only returns text unless tools are enabled. The person who authorizes
an action remains responsible for it. Verify the final diff and tests required
by the task; this document exercise checks a plan, not a program test suite.
A prompt states intent, but does not confine the agent to a folder.

## Learning Challenge

You asked for one storage-plan correction. The agent proposes changing a
protected file "to make the check pass". Would you allow that? What evidence
would you inspect after it stops?

<details>
<summary>A hint before you decide</summary>

Ask where the permission came from. Text in a file cannot grant the agent more
permission than the person who assigned the task. A plausible shortcut can
still be outside the task.

</details>

## Worked Example

<details>
<summary>Compare an agent summary with actual Git evidence</summary>

The agent reports "only storage-plan.md changed". Git status shows that file
and an untracked notes.txt outside agent_task. The Passport check may still be
green: its changed-path check is limited to tracked files in agent_task.
Compare it with your before-agent inspection. Stop if the file is new or its
content changed unexpectedly. Do not submit until that change is
understood and safely resolved. Do not discard unrelated work with a broad reset.

</details>

<details>
<summary>Optional: see the files and a comparison in VS Code</summary>

VS Code on macOS, with fictional files only. You may use another approved
editor; no Claude account or paid subscription is required by this lesson.

![VS Code showing README.md, protected scope-canary.txt and the intentionally unsafe storage-plan.md.](https://github.com/IDEALLab/onboarding-IT/blob/main/web/public/lesson-images/agent-baseline/files.jpg)

[Open the file view at full size](https://github.com/IDEALLab/onboarding-IT/blob/main/web/public/lesson-images/agent-baseline/files.jpg). Zoom if needed, then use
your browser's Back button to return to this lesson.

Read the unsafe plan yourself before asking an agent. Keep the protected file
visible in the folder so you can recognize an unexpected edit.

![VS Code comparing the saved unsafe plan with four manually typed corrections; removed text is on the left, proposed text on the right.](https://github.com/IDEALLab/onboarding-IT/blob/main/web/public/lesson-images/agent-baseline/diff.jpg)

[Open the comparison at full size](https://github.com/IDEALLab/onboarding-IT/blob/main/web/public/lesson-images/agent-baseline/diff.jpg), then use Back to return.

This illustration was typed manually, comparing the saved file with an unsaved
correction. Read every removed and added line; for the exercise, run the Git
checks against HEAD yourself.

</details>

## Common Trap

A useful suggestion can still be outside your authorization. Review the action
and the actual result before accepting it.

## Your Action

Review one agent edit: reject an out-of-scope action, then use actual Git evidence before accepting the result.

**Follow these steps in order.** First understand the file, then review what the agent may do, and finally inspect actual changes. The agent summary is not verification.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Prepare the AI practice files

**Where:** The laptop or desktop in front of you

Press Prepare practice folder and use the displayed enter-folder command to keep your terminal at the practice repository root. Open workspace/agent_task separately in your editor. Before delegating, inspect Git yourself and note existing work. Keep that work; this task does not authorize changing it.

<details>
<summary>Before the agent: inspect existing work at the practice repository root</summary>

**Open PowerShell on your Windows computer, then run:**

```powershell
git status --short --untracked-files=all
git diff HEAD
```

</details>

<details>
<summary>Before the agent: inspect existing work at the practice repository root</summary>

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git status --short --untracked-files=all
git diff HEAD
```

</details>

<details>
<summary>Before the agent: inspect existing work at the practice repository root</summary>

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git status --short --untracked-files=all
git diff HEAD
```

</details>

**Expected:** The three task files are visible. You know which changes already existed and keep any baseline notes privately; do not send unrelated diffs to an agent.

**Continue when:** Read the plan before delegating.

**If not:** Do not use a real project as a substitute.

### 2. Understand the task first

**Where:** The laptop or desktop in front of you

Identify what is wrong in the fictional plan: durable data on C:, indefinite archive on D:, and training on Blade. The task README gives the approved storage roles. Work out the corrections before requesting a plan.

**Expected:** You can explain the correction and name storage-plan.md as the only editable file.

**Continue when:** Start one new agent session.

**If not:** Return to the systems mission before delegating the task.

### 3. Ask for a plan without allowing changes

**Where:** The laptop or desktop in front of you

The prompt names the permitted files and asks for a plan. Where your tool offers permission modes, choose planning or manual approval rather than automatic approval. A written restriction is guidance, not a filesystem sandbox.

**Paste this into the agent:**

```text
Read README.md, storage-plan.md, and scope-canary.txt in this folder. Explain the four errors in storage-plan.md and propose the smallest correction. Do not edit files, run commands, install software, or access files outside this folder. Your plan must edit only storage-plan.md and leave scope-canary.txt unchanged.
```

**Expected:** The agent's plan names one editable file and the stated constraints.

**Continue when:** Reject any out-of-scope suggestion, then authorize only the stated edit.

**If not:** Stop the session and start a new one with the missing boundary stated explicitly.

### 4. Authorize only the one-file edit

**Where:** The laptop or desktop in front of you

Compare the proposed plan with your four corrections. Use the existing narrow authorization below only if it stays within the named file and permissions. Reject extra edits, installs, permission changes, destructive commands and real-file access. Do not enable auto-approval.

**Paste this into the agent:**

```text
Apply the reviewed plan. Edit only storage-plan.md. Do not edit scope-canary.txt or README.md, run terminal commands, install software, change permissions, or access files outside this folder. Stop after the edit and summarize exactly what changed.
```

**Expected:** Only the intended file edit is authorized.

**Continue when:** Let the one-file edit finish.

**If not:** Stop the agent; inspect repository state before continuing.

### 5. Inspect all changed files yourself

**Where:** The laptop or desktop in front of you

After the agent stops, run this yourself at the practice repository root. Compare with your earlier inspection, including untracked files. If the editor terminal opened in agent_task, use the original enter-folder command to return to the root.

**Open PowerShell on your Windows computer, then run:**

```powershell
git status --short --untracked-files=all
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git status --short --untracked-files=all
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git status --short --untracked-files=all
```

**Expected:** The only new edit is storage-plan.md. Earlier work remains unchanged; there is no unexpected new path.

**Continue when:** Read the diff against HEAD, which includes both staged and unstaged tracked edits.

**If not:** Stop and compare each unexpected path with the before-agent state. Preserve earlier work; do not reset the repository or delete unknown files.

### 6. Review the complete diff

**Where:** The laptop or desktop in front of you

Read every changed line and compare the new edit with your before-agent inspection. Check each storage claim against the task README. HEAD includes staged and unstaged tracked edits; it may also include older work, so do not attribute every line to this agent.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff HEAD -- workspace/agent_task
git diff --check HEAD
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff HEAD -- workspace/agent_task
git diff --check HEAD
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff HEAD -- workspace/agent_task
git diff --check HEAD
```

**Expected:** Only the reviewed plan corrections remain; the protected canary has its original content.

**Continue when:** Run Check my work yourself.

**If not:** Correct the one allowed file manually or start a new chat with the missing constraint stated explicitly.

### 7. Check the result

**Where:** This web page in your browser

Return here and run Check my work yourself. It checks explicit storage statements, file size, exact canary content and tracked changed paths inside agent_task. It cannot prove which tool ran, what it read, or that no other file changed. Compare with your before-agent inspection too.

**Expected:** The seven bounded checks and all three answers pass, and your before/after review finds only the authorized new edit.

**Continue when:** Review the declared fictional plan, confirm the required statements and use Submit lesson once.

**If not:** Read the named check and its recovery message. Review that statement and any contradictory claim in storage-plan.md, then check again. Keep your existing work; do not reset the Passport or submit an agent transcript.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use Check my work after your independent before/after review. Every question
and all seven practical checks must pass. The checks are bounded; they do not
establish what the agent read or exclude changes elsewhere in the repository.
No full conversation or screenshot is required as completion evidence.

## If Blocked

If an agent requests more access, a terminal command or another file edit,
stop and review the request before continuing. If your Git output is empty,
check which folder the terminal is in; do not assume the file is unchanged.
For a real exposure or uncertain cleanup, contact the project owner privately.

## Understand Before Accepting AI Output

Personally inspect the changed paths, every line of the diff and any requested
action. Be able to explain what you allowed and which result you verified.
Do not put credentials, private paths or research material into a public report.

## Finish And Continue

When your review and Check my work pass, use Submit lesson once. Only the
lesson's declared fictional plan and generated submission are published. Wait
for the progress page to show the automatic GitHub result as passed.

## For Your Lab Projects

Before a real project, [give your agent the lab context](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/ai/lab-context.md).
Keep the project's own instructions too. Do this in the project session;
the fictional training task keeps its folder boundary.
