# Scripps Hackathon Starter

A ready-to-fork template for participants of the [**Scripps Research
2026 Computational Biology & Bioinformatics Hackathon**](https://scripps-cbb.github.io/)
(May 29 – June 1, La Jolla).

It gives you, out of the box:

- A **Claude Code** workspace pre-configured with two specialized skills:
  - `/hackathon-aws` — full context on the hackathon's AWS account
    (VPC, EC2, S3, EICE SSH, Bedrock)
  - `scripps-garibaldi-hpc` — Garibaldi cluster conventions, Slurm
    templates, GPU job patterns
- **Setup guides** for both platforms ([AWS_SETUP.md](AWS_SETUP.md) and
  [HPC_SETUP.md](HPC_SETUP.md))
- **Three "Hello World" exercises** ([hello-world/](hello-world/)) that
  get you fluent with Claude Code (slash commands + auto mode) and
  then validate your HPC and AWS accounts

---

## Never used GitHub before? Start here.

Welcome! This page is the homepage of a **repository** — a folder of
files tracked by Git. You don't need to learn Git to use this template.
The fastest path:

1. **Get the code on your laptop.** Pick whichever path fits you:
   - **Fork (recommended if you want to keep your work).** Sign in to
     GitHub, click **Fork** at the top right of the repo page, then
     clone *your fork* — e.g. `git clone https://github.com/<your-username>/scripps-hackathon-starter`.
     This gives you a personal copy you can commit to all weekend, share
     with teammates, and revisit after the hackathon. Drop your project
     code in a new folder of your fork (e.g. `my-project/`) so it lives
     alongside the starter setup.
   - **Clone read-only.** `git clone https://github.com/scripps-cbb/scripps-hackathon-starter`
     — quickest if you already have a git account but don't plan to
     push code back.
   - **Download ZIP (no GitHub account needed).** Click the green
     **`<> Code`** button → **Download ZIP** → unzip it somewhere you
     can find again. Lowest friction; you won't be able to push your
     code back to GitHub from this copy.
2. **Install Claude Code** if you haven't already:
   <https://www.claude.com/product/claude-code>
3. **Open this folder in Claude Code.** On Mac/Linux: `cd
   scripps-hackathon-starter && claude`. On Windows: open the folder in
   VS Code with the Claude Code extension installed.
4. Run the **Hello World** exercises below in order. They take ~15
   minutes total and tell you exactly which piece (if any) of your
   setup needs attention.

You'll spend almost all of your hackathon time *talking to Claude in
plain English* — telling it what you want, and letting it run the
commands. The skills in this repo are what make that work for AWS and
HPC specifically.

> **Stuck?** Open Claude Code in this folder and just ask. The skills
> teach Claude what's in this repo, so questions like "what does this
> file do?" or "I got this error — what should I try?" work well.

---

## What's in this repo

```
.
├── README.md                       <- you are here
├── AWS_SETUP.md                    <- set up AWS CLI + SSO + the skill
├── HPC_SETUP.md                    <- set up Garibaldi HPC access
├── test_skill.sh                   <- end-to-end AWS smoke test (bash)
├── hello-world/
│   ├── README.md                   <- three-exercise walkthrough
│   ├── hello_claude.md             <- "drive Claude Code" (slash cmds, modes)
│   ├── hello_hpc.slurm             <- "does Slurm work?" (Garibaldi)
│   └── hello_aws.py                <- bonus: "does AWS Bedrock work?" (Python)
└── .claude/
    ├── commands/
    │   └── hackathon-aws.md        <- the /hackathon-aws slash command
    └── skills/
        └── scripps-garibaldi-hpc/
            └── SKILL.md            <- auto-loaded HPC skill
```

---

## Quickstart

> **TL;DR — one-prompt smoke test (for experienced users).** Open Claude
> Code in any folder, paste the prompt below, and it'll clone this repo
> and run the Hello World end-to-end. **New to all this? Skip this box
> and follow the four numbered steps below instead — they explain what
> you're doing as you go.**
>
> ```text
> Clone https://github.com/scripps-cbb/scripps-hackathon-starter onto
> my Desktop, cd in, then run the Hello World as a smoke test:
>
> - Skip hello_claude.md (the Claude Code tour) — I already know the
>   basics.
> - Lint hello-world/hello_hpc.slurm with `bash -n` and report any
>   issues. Don't try to submit it.
> - Run ./test_skill.sh against my AWS SSO profile <MY_PROFILE>. If my
>   token is expired, tell me to run `aws sso login --profile
>   <MY_PROFILE>` and wait for me to confirm before retrying. The
>   script will create an S3 bucket, briefly launch a t3.micro, and
>   terminate it — that's expected.
> - If you can pip install boto3, also run hello-world/hello_aws.py
>   with my profile to confirm Bedrock works.
> - Stop and ask me before terminating or deleting anything I didn't
>   create in this session.
>
> End with a punch list of any failures and what I should do next.
> ```
>
> Replace `<MY_PROFILE>` with your AWS SSO profile name (both places).
> No profile yet? Walk through [AWS_SETUP.md](AWS_SETUP.md) first, then
> come back here.

### 1. Get fluent with Claude Code (5 minutes)

Open this repo in Claude Code and follow
[hello-world/hello_claude.md](hello-world/hello_claude.md). You'll try
slash commands, switch into auto-accept-edits / plan mode, and run
**auto mode** so you've seen all of it once before it matters.

### 2. Set up the HPC (5 minutes once your account is provisioned)

Follow [HPC_SETUP.md](HPC_SETUP.md). At the end you'll `sbatch
hello_hpc.slurm` and see your job run on a Garibaldi compute node.

### 3. Set up AWS (10 minutes, one-time)

Follow [AWS_SETUP.md](AWS_SETUP.md). At the end you'll run:

```bash
./test_skill.sh
```

It creates an S3 bucket, reads a public dataset, launches and terminates
a tiny EC2 instance, and tells you PASS/FAIL for each step.

### 4. Talk to Claude

Open this repo in Claude Code and try any of these:

```text
/hackathon-aws launch a t3.medium and SSH into it

write me an sbatch script for Garibaldi that runs train.py on 1 GPU for 4 hours

create an S3 bucket called scrippsresearch-<myname>-hackathon and upload my results folder

I got "Token has expired" — what now?
```

The first request hits the AWS slash command. The second auto-loads
the HPC skill. The third works with either, depending on context. The
fourth is just a normal conversation — Claude already knows what to do
because the skills tell it.

---

## Shared hackathon data

The organizers have pre-loaded project datasets into a shared S3
bucket: **`s3://scrippsresearch-hackathon/`**. Once your SSO is set up
([AWS_SETUP.md](AWS_SETUP.md)) and `aws sso login` has succeeded, you
can browse and download with your own profile — no extra credentials.

```bash
# See what's available
aws s3 ls s3://scrippsresearch-hackathon/ --profile <your-profile>

# Peek inside a specific project
aws s3 ls s3://scrippsresearch-hackathon/allen/ --profile <your-profile>

# Pull a project's data down to your laptop (or EC2 / HPC scratch)
mkdir -p data/allen
aws s3 sync s3://scrippsresearch-hackathon/allen/ data/allen/ \
  --profile <your-profile>
```

Each prefix is one team's project. **Start by reading the project's
own docs** for context, file conventions, and what the inputs actually
mean:

| Prefix       | Topic                              | Start here                                                                                  |
|--------------|------------------------------------|---------------------------------------------------------------------------------------------|
| `allen/`     | PQBP1 hexamer cryo-EM + docking    | `PQBP1_Hexamer_IM_README.md` and `_UPLOAD_NOTES.md` inside the prefix                       |
| `heberling/` | Siglec6 structural work            | `Hackathon Materials Notes JLH.pdf` |

Quick way to read a project README without downloading the whole thing:

```bash
aws s3 cp s3://scrippsresearch-hackathon/allen/PQBP1_Hexamer_IM_README.md - \
  --profile <your-profile>
```

(The trailing `-` streams to stdout.)

> **Big datasets?** Copy only what you need. `aws s3 cp --recursive`
> and `aws s3 sync` both accept `--exclude '*'` / `--include 'pattern'`
> so you can grab e.g. just the `.pdb` files. For 10+ GB downloads,
> consider running the `sync` from an EC2 instance instead of your
> laptop — S3 → EC2 traffic in `us-west-2` is free via the VPC
> gateway endpoint.

---

## How the Claude tooling works (in 60 seconds)

There are two kinds of context-providers in this repo:

- **Slash commands** live in `.claude/commands/`. You invoke them
  explicitly: `/hackathon-aws <your request>`. Use this when you want
  to be sure Claude has the full AWS context loaded.
- **Skills** live in `.claude/skills/<name>/SKILL.md`. Claude loads
  them automatically when your question matches the skill's
  description. You don't type anything special — just ask about
  Garibaldi and the cluster skill kicks in.

Both files are plain Markdown — open them and read along if you're
curious. Editing them changes how Claude behaves in your session.

---

## Personalize before you start

A few values in this template point at the maintainer's defaults.
Update them once and the rest of the toolchain follows:

| File | What to change |
|---|---|
| [test_skill.sh](test_skill.sh) | Set `PROFILE` to your SSO profile name, and `BUCKET` to a name that includes your username. |
| [hello-world/hello_aws.py](hello-world/hello_aws.py) | Default `--profile` argument (or pass it on the CLI). |
| [.claude/commands/hackathon-aws.md](.claude/commands/hackathon-aws.md) | The skill references `inewman-wsl` as the example profile — when you start a Claude session, just tell it "use profile `<yours>` for all AWS commands" and it will. No file edit needed. |

If you'd like Claude to remember your profile across sessions, ask it
to save a memory: *"Remember that my AWS profile is `bgood-scripps`."*

---

## Where to go from here

- Hackathon homepage and schedule: <https://scripps-cbb.github.io/>
- AWS account ID / SSO portal: see [AWS_SETUP.md](AWS_SETUP.md)
- HPC contact: `hpc@scripps.edu` (for Garibaldi account requests)
- Claude Code docs: <https://docs.claude.com/en/docs/claude-code>

Good luck and have fun. The whole point of the weekend is to try
something you wouldn't normally try — the tools in this repo are here
so the **infrastructure** isn't what slows you down.
