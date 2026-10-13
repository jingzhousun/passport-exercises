# Mission: Review A One-GPU Euler Plan

## Outcome

Choose the next graphics processor (GPU) request from the supplied measurements.
You already know how to read a job request and calculate total system RAM.

## Concept

The measurements in this lesson are invented. No GPU allocation is needed.

A GPU is an accelerator for suitable calculations. A Slurm GPU request reserves
it with supporting CPU, memory and time resources. `es_fuge` is the lab computing
share used for this review. A partition is a group of compute nodes; keep its
selection automatic here.

A reserved GPU can sit idle. Find what limits useful work before reserving more.
System RAM is used by the CPU-side program; GPU memory (VRAM) is on the
accelerator. `--mem-per-cpu` changes system RAM, not VRAM. Throughput is useful
work completed per second.

## Learning Challenge

### The GPU waits for input

A fictional one-GPU run spends 60% of its time waiting for the next input batch.
What would you investigate or change first, and why? The table tells you
where time is spent; it does not identify the precise cause.

<details>
<summary>A hint for the input wait</summary>

Adding an accelerator helps only if it can receive useful work. Inspect the
waiting stage and approved data placement before changing GPU count.

</details>

### Choose supporting resources

After the input problem is fixed, three runs use the same representative
workload and configuration. Assume one task on one node and exactly the CPUs
requested. A supplied CPU comparison found four useful threads. The GPU in
this fictional case has 24 GiB of VRAM.

| Measurement | Runs A / B / C |
| --- | --- |
| Elapsed (minutes) | 12 / 13 / 14 |
| System RAM peak (GiB) | 10 / 11 / 12 |
| GPU VRAM peak (GiB) | 16 / 17 / 18 |

These are supplied application measurements, including all its processes,
not a top-level `MaxRSS` field. Headroom means room for modest variation above
the observed peak. Choose a next request for the same workload, not every
future dataset.

<details>
<summary>A hint for memory and time</summary>

Multiply allocated CPUs by memory per CPU. Compare that system-memory total
and the time limit with the largest values in the table. GPU VRAM cannot make
up for a shortage of system RAM.

</details>

### Is a second GPU useful enough?

A separate controlled comparison keeps the input, amount of work and output
quality equivalent. Rates cover the entire timed run, including setup and
waiting. Repeated trials give the supplied representative rates:

| GPUs reserved | Useful throughput |
| --- | --- |
| 1 | 100 samples per second |
| 2 | 110 samples per second |

For the same amount of work, does the small speed gain justify twice the
reserved hardware? GPU reservation time is GPU count multiplied by run time.

<details>
<summary>A hint for the comparison</summary>

Speedup is the new throughput divided by the old throughput. For fixed work,
compare GPU count divided by throughput. Faster completion does not necessarily
mean less total GPU reservation time.

</details>

## Worked Example

Try your own request before opening the script model in the practical step.

## Common Trap

A starter limit is a ceiling, not a target. For real work, review representative
measurements and any multi-GPU request with your supervisor.

## Your Action

Use the supplied measurements to choose a next request, then review the fictional script locally.

**Follow these steps in order.** All measurements on this page are fictional. This review needs no Euler connection or GPU allocation. The planning decisions and local script review are separate exercises.

**New to text commands?** A command is a line of text that tells a
computer to do one task. A terminal is the text application in which a
shell reads that command. Open PowerShell on Windows or the application
named Terminal on macOS or Linux. The application starts the correct
shell automatically; do not install a separate Bash or zsh application. Read
[Terminal and command basics](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/core/command-line-basics.md)
before continuing if these words are new.

### 1. Read the three comparisons

**Where:** This web page in your browser

Use the fictional tables above. Before revealing a hint, choose what you would investigate or request and why. Keep the observed system RAM separate from memory on the GPU.

**Expected:** You have a reason for each decision, rather than only choosing the largest permitted request.

**Continue when:** Review the practice file.

**If not:** Use the short hint next to the relevant table; no external tutorial is required.

### 2. Review the local script

**Where:** The laptop or desktop in front of you

In a local Passport, Prepare practice folder creates workspace/slurm/gpu_job.slurm.txt. For the practical exercise, keep one named GPU on es_fuge, remove the forced partition and --mem, and retain unique logs. Choose CPU, memory-per-CPU and time values you can justify from the supplied measurements, within the starter limits: 1-16 CPUs, at most 64 GiB total system RAM and a positive time no longer than four hours. The checker verifies bounds; compare the request with the measurements yourself. Save a UTF-8 file smaller than 100000 bytes. Use ASCII digits without signs for CPU, memory and time values.

<details>
<summary>Compare one reasonable request for the supplied measurements</summary>

**Put this in the named Bash file:**

```bash
#!/usr/bin/env bash
# FICTIONAL REVIEW FIXTURE - DO NOT SUBMIT OR EXECUTE
#SBATCH --job-name=passport-gpu
#SBATCH --account=es_fuge
#SBATCH --gpus=rtx_4090:1
#SBATCH --cpus-per-task=4
#SBATCH --mem-per-cpu=4G
#SBATCH --time=00:20:00
#SBATCH --output=logs/%x_%j.out
#SBATCH --error=logs/%x_%j.err

# Review only; no training program is supplied.
```

</details>

**Expected:** The text describes a one-GPU request; you have not run or submitted it.

**Continue when:** Compare with the optional model only after choosing your values.

**If not:** Never execute the intentionally unsafe practice file. Open only this fictional file, not a research script.

### 3. Inspect what you changed

**Where:** The laptop or desktop in front of you

From the practice repository root, inspect the diff of the named file. This is a text review, not a Slurm syntax or performance test. The current checker enforces starter bounds; it cannot establish whether a real workload needs them. Slurm ignores directives after the first shell command. Keep every #SBATCH line before commands, with one unquoted long option and literal value per line. Keep each option only once. Use the supplied options; optional --nodes and --ntasks must each be 1.

**Open PowerShell on your Windows computer, then run:**

```powershell
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Open Terminal on your Mac; zsh starts inside it automatically. Then run:**

```zsh
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Open Terminal on your Linux computer; Bash normally starts inside it automatically. Then run:**

```bash
git diff -- workspace/slurm/gpu_job.slurm.txt
```

**Expected:** Only the intended fictional script changed; the plan stays within the lab review policy.

**Continue when:** Answer the three questions, then use Check my work. Submit only after reviewing the generated exercise result.

**If not:** If unsure, leave the file unsubmitted and use Passport help. Do not request a real GPU merely to pass.

The Passport presents the questions and required confirmation in the
browser. Do not create or edit a submission JSON file by hand.

## Check Your Work

Answer the three decisions and review the fictional file with Check my work.
The check covers starter limits; it does not execute the script or prove performance. A real project needs its
own representative measurements and review.

If needed, open only [the GPU policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/euler-share.md#required-behavior)
and return here. No real logs, screenshots, account names or research data are
requested for this exercise.

## If Blocked

Use the hint beside the relevant table, then retry the sample question. If the
local script is unclear, leave it unsubmitted and use the help request in your
real Passport. Never paste real logs, private paths or credentials.

If needed, open only [the GPU policy](https://github.com/IDEALLab/onboarding-IT/blob/main/docs/policy/euler-share.md#required-behavior)
and return to this review. If an AI agent proposes a request, check its arithmetic
and every changed directive yourself before accepting it.

## Understand Before Accepting AI Output

Check the CPU times memory calculation, time headroom and every directive yourself.
The script check rejects repeated or late directives and options outside this
exercise. It permits only one node and one Slurm task per job. It does not
evaluate the program body, software compatibility or actual performance.
Review these separately before any real submission.

## Finish And Continue

After a successful check, review and submit the generated exercise result.
No live GPU trial is required. Existing Passports keep their original criteria.
