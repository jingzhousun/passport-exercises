# Mission: Cap And Calculate Euler Job Arrays

## Outcome

Calculate an array's peak demand with another job already active, then choose
a cap that fits a supplied budget. Keep the local guided file repair.

## Concept

A job array repeats a job for several inputs. Its range gives the total number
of tasks; the number after `%` is the concurrency cap, limiting how many can
run together. Each running
task requests its own CPUs and system memory. Your other jobs count too.
A distinct log name identifies each task and keeps its output separate.

## Learning Challenge

Plan the proposal at the calculation step, then answer the three questions.
You can use paper or a calculator.

The guided file repair and the planning example are separate. Keep the
practice file at its required cap of one; do not put the proposed caps into it
or submit an array to Euler.

## Worked Example

<details>
<summary>A reminder for the calculation</summary>

Count simultaneous array tasks first, then work out their CPU and memory
requests. Add the resources held by every other job. Compare CPU and memory
separately with the budget; fitting one limit is not enough.

`--mem-per-cpu` requests memory for each allocated CPU. `--mem` requests memory
per node. In this example each array task uses one node and one Slurm task.
Do not use both memory options in the same script.

</details>

## Common Trap

A planning cap is not the required cap-one file repair. Keep them separate.

## Your Action

Correct the fictional Slurm array practice file, add a concurrency cap, and make every task log name unique.

**Follow these steps in order.** The supplied file is deliberately unsafe. Edit it locally and never submit it to Euler.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Understand an array and its concurrency cap

**Where:** This web page in your browser

Read the range and cap distinction above. This is local review only; no array is submitted.

**Expected:** You can distinguish total task count from the maximum running at once.

**Continue when:** Open the deliberately unsafe local practice file.

**If not:** Do not submit a real array until you can calculate its simultaneous resource total.

### 2. Prepare the array practice file

**Where:** The laptop or desktop in front of you

Press Prepare practice folder, enter it, and open workspace/slurm/array_job.slurm.txt.

**Expected:** The unsafe practice file is open in the separate practice repository.

**Continue when:** Inspect it without submitting.

**If not:** Do not create your own replacement script or use Euler for this exercise.

### 3. Inspect the cap and log names

**Where:** The laptop or desktop in front of you

Read the array and two log directives in the unsafe local file. Which setting bounds simultaneous demand? Which filename placeholders identify the parent and index? Compare your reasoning with the repair steps afterwards; do not submit this file.

**Expected:** You can explain the missing concurrency cap and why parent/index labels make array logs easier to trace.

**Continue when:** Edit only the required directives.

**If not:** Review the array and log-name explanation before editing.

### 4. Add a small concurrency cap

**Where:** The laptop or desktop in front of you

Replace the unsafe array directive with the exact line below. It creates ten tasks, numbered 0 through 9, and allows at most one to run at a time.

<details>
<summary>Show the required cap-one repair</summary>

**Put this in the named Bash file:**

```bash
#SBATCH --array=0-9%1
```

</details>

**Expected:** The directive is exactly --array=0-9%1.

**Continue when:** Make the logs unique.

**If not:** Do not use an uncapped range or a zero cap.

### 5. Use parent and task IDs in logs

**Where:** The laptop or desktop in front of you

Replace both log directives with the two exact lines below. %A is the parent job ID and %a is the array task index.

<details>
<summary>Show the required parent/index log lines</summary>

**Put this in the named Bash file:**

```bash
#SBATCH --output=logs/%x_%A_%a.out
#SBATCH --error=logs/%x_%A_%a.err
```

</details>

**Expected:** Each array task has a distinct output and error path.

**Continue when:** Inspect the local diff.

**If not:** Correct both settings before pressing Check my work.

### 6. Plan a different array on paper

**Where:** This web page in your browser

Plan a different array on paper: 12 tasks, cap 3, 2 CPUs per task and 3 GiB per CPU. Another job holds 2 CPUs and 5 GiB. The fictional combined budget is 10 CPUs and 20 GiB. Assume one node and one Slurm task per array task, with allocated CPUs matching the request.

**Expected:** Compare peak requested CPUs and system memory with both fictional limits. This is not your Euler entitlement. Keep the practice file at cap one; no job is submitted.

**Continue when:** Answer the three planning questions after reviewing the local file. For the memory-option comparison, replace the proposal's --mem-per-cpu=3G with --mem=3G; do not add both.

**If not:** If a calculation does not fit, reduce concurrency on paper. Do not change CPU or memory estimates just to fit a budget: a real program needs measured evidence first.

### 7. Review the edited file

**Where:** The laptop or desktop in front of you

Confirm that only the fictional practice file changed and that no command submitted it. Slurm ignores directives after the first shell command. Keep every #SBATCH line before commands, with one unquoted long option and literal value per line. Keep each option only once. Use the supplied options; optional --nodes and --ntasks must each be 1.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff -- workspace/slurm/array_job.slurm.txt
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff -- workspace/slurm/array_job.slurm.txt
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff -- workspace/slurm/array_job.slurm.txt
```

**Expected:** The diff changes only the array cap and the two log names.

**Continue when:** Run Check my work.

**If not:** Remove every unrelated change before continuing.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Answer the three planning questions and review the declared fictional file.
**Check my work** checks both your answers and the cap-one/log repair on this
computer. All three answers and every file check must pass before **Submit
lesson** is available. Feedback explains a failed calculation; correct your
answer and check again. Nothing in this lesson submits a job to Euler.

## If Blocked

Keep the guided file repair at `--array=0-9%1`. If a calculation fails, count
running tasks, add the separate job, then check CPU and memory against their
budgets. A planning cap of two does not change the required cap-one file repair.

If the file check fails, inspect the named file and its diff. Keep it smaller
than 100000 bytes; remove only an understood accidental addition. Do not reset
the repository, recreate your Passport, submit an array or change an account.
Use the local Passport's public help request if the expected result stays unclear;
exclude credentials, private logs and real research files.

Useful references, only if needed; return to this lesson afterwards:

- [Array review](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/labs/euler-job-arrays.md): range, cap and logs.
- [Slurm reference](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/reference/euler/slurm.md): job lifecycle.

## Understand Before Accepting AI Output

Calculate the combined request yourself. An array's cap does not constrain
other jobs. A budget is a ceiling, not a target. The numbers in this lesson are
fictional; an agent must not treat them as permission to launch real jobs or
reduce a real memory estimate without measurements.

## Finish And Continue

When **Check my work** passes, use **Submit lesson** once. Only this lesson's
generated answers, receipt and declared fictional file are published. Continue
when the progress page shows the automatic GitHub result as passed; a check
on this computer alone is not completion.
