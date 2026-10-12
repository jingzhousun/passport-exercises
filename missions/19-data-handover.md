# Mission: Create A Recoverable Project Handover

## Outcome

Give a successor enough information to locate the required files and check a
result without the departing researcher's computer or personal login.

## Concept

A project handover is a transfer of ownership with enough information for
the authorized successor to continue. A code revision identifies the exact
committed files. An environment definition records the required software.

A handover connects the code version, required inputs, software setup and a
verifiable result. A filled field is a useful pointer, not proof that the
pointer works. Temporary work and approved source data have different lifetimes.

## Learning Challenge

The author can run a tiny fictional project on their laptop. Its handover says
"the command passed", but the only input copy is in their temporary folder.
What would prevent you from continuing after they leave?

Review one inventory and three decisions. If Git and Python already work, you
may also try the supplied project in a fresh clone. This is optional: the Data
Steward route does not require a new Python setup lesson.

## Worked Example

<details>
<summary>What to verify before saying the handover works</summary>

Check the exact code, input identity and setup. Run a known small check, compare
its actual output with the expected values, and state what remains unverified.
A zero exit code alone does not establish that the right input or result was
used. Access and retention still need their owners' decisions.

</details>

## Common Trap

An exit code of zero can accompany the wrong result. Compare expected values
and preserve the original inputs before retiring temporary work.

## Your Action

Complete one fictional handover document using the prepared inventory. Review the three decisions; a fresh-clone rerun is optional.

**Follow these steps in order.** Use only the supplied fictional project. No personal accounts, real paths or datasets belong in this exercise.

### 1. Prepare the fictional handover

**Where:** The laptop or desktop in front of you

Press Prepare practice folder. It prepares the worksheet and a separate fixed project, and shows its actual revision. Open workspace/handover/project-handover.md in the practice folder.

**Expected:** The worksheet and fictional inventory are available.

**Continue when:** Read the inventory before filling the worksheet.

**If not:** Preserve any existing or altered folder and request help; do not replace it with real project files.

### 2. Find what the successor needs

**Where:** This web page in your browser

The supplied inventory contains verify.py, inputs/measurements.csv and environment.json. The environment declares Python 3.9 or newer, with no external packages. scratch/ and .venv/ are temporary and are not in the transfer.

**Expected:** Distinguish required source/input/setup from recreated local state.

**Continue when:** Compare each handover field with the inventory.

**If not:** A complete-looking document is insufficient if its named files cannot be obtained.

### 3. Complete the fictional handover

**Where:** This web page in your browser

Keep each label once on its own line. Choose fictional owners and a limitation. Copy the inventory revision and file identities, then record the setup and verification commands for your operating system. Use a valid future planned deletion date for the fictional temporary copy.

<details>
<summary>Show the fixed inventory fields</summary>

**Put this in the named Markdown file:**

```markdown
Repository: local fictional fixture

Revision: 4e45a59f4a09d7c069d8af34b5d724f7c7c513cf

Main approved data location: inputs/measurements.csv

Temporary locations to remove: scratch/

Environment definition: environment.json

Expected result: measurements=3 total=12
```

</details>

<details>
<summary>Show setup and verification fields for macOS or Linux</summary>

**Put this in the named Markdown file:**

```markdown
Setup command: python3 -m venv --without-pip .venv

Verification command: ./.venv/bin/python -I verify.py
```

</details>

<details>
<summary>Show setup and verification fields for Windows</summary>

**Put this in the named Markdown file:**

```markdown
Setup command: python -m venv --without-pip .venv

Verification command: & .\.venv\Scripts\python.exe -I verify.py
```

</details>

**Expected:** The document describes only this fixed project and states what remains unverified.

**Continue when:** Review the document before checking it. Do not claim a personal rerun if you use the supplied observation.

**If not:** Do not invent access or claim a run that you did not observe.

### 4. Optional: try a fresh clone

**Where:** The laptop or desktop in front of you

If Git and Python 3.9+ already work, open Optional: reproduce in a fresh clone under the prepared inventory. Review and run that generated command. Stop on an existing target; the original project and your terminal directory stay unchanged.

**Expected:** The fresh clone prints measurements=3 total=12. Compare both values and the exit status.

**Continue when:** An environment is recreated, not copied. Record only the result personally observed.

**If not:** You can use the supplied observation for this packet without claiming a personal run. Do not install Python solely for this optional task.

### 5. Decide whether the result matches

**Where:** This web page in your browser

The maintainer's fresh-clone observation is measurements=3 total=12. A deliberately changed input prints measurements=3 total=13 even though the command exits successfully. Decide what the handover should claim.

**Expected:** A successful command and a reproduced result are different claims.

**Continue when:** Use the questions to choose the next action for a mismatch.

**If not:** Do not change the expected result merely to make a check appear successful.

### 6. Separate retained inputs from temporary copies

**Where:** This web page in your browser

The fictional information owner must retain inputs/measurements.csv. Only scratch/ is named in the temporary-copy plan. Keep an access owner, retention owner, future review date and one unresolved limitation. This exercise grants no approval to delete or revoke access.

**Expected:** The next person can reproduce again after temporary work is retired.

**Continue when:** Review the packet and answer the three decisions.

**If not:** For a real unresolved ownership or retention decision, stop and contact the project owner privately.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Use Check my work to verify the declared fictional document and project inventory.
All three decisions and both computer checks must pass before Submit lesson
is available. Neither check executes a document command or verifies real access.

## If Blocked

Use the supplied observation if the optional project or interpreter is absent.
Never substitute a real research dataset. A real missing-access or retention
decision needs the project owner privately, not credentials in a public issue.

## Understand Before Accepting AI Output

An agent can format the packet. Personally compare its locations, revision,
setup and expected result with available evidence. Do not accept invented access
or certify a run from a plausible sentence.

## Finish And Continue

Submit lesson once after checking your fictional document and answers.
Wait for the automatic GitHub result before continuing. Existing older
Passports retain their original handover criteria.
