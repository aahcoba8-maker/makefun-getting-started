# Getting started with make.fun

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/aahcoba8-maker/makefun-getting-started/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![reward](https://make.fun/badge/bring-the-humans-02/aahcoba8-maker/makefun-getting-started/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

make.fun is a place where people team up with AI coding agents to build software for cash bounties. You choose the task and guide the work; your agent helps build the project. Bounties pay rewards in USDC on Solana, and each one has its own brief, deadline, and entry rules.

> **New here?** [Create your account with my referral link](https://make.fun/r/gh9tewpq). My referral code is `gh9tewpq`.

## Contents

- [How make.fun works](#how-makefun-works)
- [What you need](#what-you-need)
- [1. Create your account](#1-create-your-account)
- [2. Pick a bounty](#2-pick-a-bounty)
- [3. Get the kit](#3-get-the-kit)
- [4. Build your entry](#4-build-your-entry)
- [5. Submit it](#5-submit-it)
- [6. Check it, fix it, resubmit](#6-check-it-fix-it-resubmit)
- [7. Claim your reward](#7-claim-your-reward)
- [A realistic first week](#a-realistic-first-week)
- [Common mistakes that get entries rejected](#common-mistakes-that-get-entries-rejected)
- [Or let your agent do the whole thing](#or-let-your-agent-do-the-whole-thing)
- [Earn with your own referral link](#earn-with-your-own-referral-link)
- [Ringkasan Bahasa Indonesia](#-ringkasan-bahasa-indonesia)
- [Questions](#questions)
- [Links](#links)

## How make.fun works

A bounty is a time-limited software competition: read the task, make an entry, and submit it before the deadline. The process moves through these stages:

| Stage | What happens |
| --- | --- |
| Open | The task accepts entries. Read its brief and start your work only after this point. |
| Submitted | An entry is a public GitHub repository at one chosen commit, with the agent-session transcripts that produced it. Some bounties also request a source bundle. |
| Checked | Automated and, where applicable, human checks look for compliance with the bounty rules. |
| Scored | Valid entries are assessed against the task; the ranking determines who can claim the reward. |
| Paid | The winner claims USDC from the bounty escrow to their Solana wallet. |

Most bounties are free to enter. When a bounty opens, its full reward is locked in make.fun’s on-chain Solana escrow program. Session transcripts help show how the work was made and keep judging fair. If entries tie, the earlier qualifying entry takes precedence.

## What you need

- **An AI coding agent.** Claude Code, Codex, Cursor, Copilot, Gemini CLI, and similar tools can help you create and change a project. Pick one you can run comfortably.
- **A GitHub account.** Entries are public repositories, so you’ll need to publish your work and point make.fun to the exact commit.
- **Node.js 22.** The make.fun kit command-line tool runs with Node.js. Install a current version 22 release before using the CLI.
- **A Solana wallet.** You’ll connect one to your account to receive a reward if you win. Keep its recovery details private; never paste secrets into a chat or repository.

You don’t need to be a professional programmer. The key skills are understanding the task, checking your agent’s work, and making sure the finished project follows the bounty rules.

## 1. Create your account

Start at [make.fun using my referral link](https://make.fun/r/gh9tewpq). You can sign in with GitHub, Google, Apple, Discord, or a Solana wallet, depending on the options shown. If you already have an account, sign in instead of making a duplicate.

Fill out your profile so other people can recognize your work. In account settings, link the GitHub account where you’ll host entries and connect the Solana wallet you want to use for rewards. Check that the GitHub identity is the one you intend to publish from.

When you use the bounty kit’s CLI for the first time, connect it to your make.fun account. From the kit directory, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

The command displays a one-time authorization code and instructions. Open the page it provides, sign in if asked, and approve that code. The CLI can then identify your account for actions such as checking or submitting entries. Treat the code as temporary account access: approve it yourself and do not share it.

## 2. Pick a bounty

Browse the [bounty board](https://make.fun) and filter or browse by category to find a task that matches your interests and the time you have. A small, clearly scoped first project is often easier to finish than an ambitious one.

Open the bounty page and read it from top to bottom before you start. It explains the requested outcome, deadline, reward, required files or technologies, submission format, and judging criteria. Pay particular attention to restrictions and required proof. If anything is unclear, check the bounty’s linked discussion or ask through its listed community channel before investing a lot of time.

The deadline matters: plan enough time to build, inspect, run the required checks, and submit. A polished project that arrives after the cutoff may not qualify.

## 3. Get the kit

When a bounty offers a kit, open a terminal and download it using the slug from that bounty’s URL:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
```

Replace `<bounty-slug>` with the actual slug, without the angle brackets. The extracted folder contains the files and command-line tools for that competition. Read `RULES.txt` before doing any work: it contains the bounty rules in their authoritative wording. Don’t rely on a paraphrase if the kit’s copy says something more specific.

Some kits include a local grading or validation command. Run it as described in the kit to catch issues while you work. A local result is useful feedback, but follow the official submission process and deadline too.

## 4. Build your entry

Wait until the bounty status is **Open** before starting the agent session that will create your entry. The recorded session should be the one that builds the submitted work; starting too early can make an otherwise good project ineligible.

Create a public GitHub repository and add an open-source license. MIT is a straightforward choice for many small projects. Include its SPDX identifier line, exactly `SPDX-License-Identifier: MIT`, in the license file so automated checks can recognize it. Make sure the chosen license fits your project and the bounty requirements.

Tell your agent what the task asks for, share the relevant rules, and work through the project together. Review the result: try the main features, inspect important files, and ask the agent to fix problems you find. The submitted session transcripts are matched against the code, so they should reflect the actual work in the repository.

If a kit contains starter files, treat them as scaffolding or examples to build on. Simply submitting unchanged starter material is not a completed entry. Add the functionality and original work the bounty requests.

## 5. Submit it

Commit the version you want judged and push it to GitHub. Copy the full commit SHA; that pins the submitted project to one exact snapshot even if you continue working afterward. Keep the repository public so the checks and judges can access it.

From the kit directory, create a bundle of the agent transcripts. Adjust the repository path if your folder layout differs:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

Run the kit checks on both the repository and the transcript bundle before entering:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Read the full output and fix any reported issue before submitting. A rejected submission still uses one of your allowed entries for that day, so checking first gives you a chance to catch easy-to-fix problems. Then submit with the bounty slug, public repository URL, exact commit SHA, bundle path, and your make.fun CLI keypair:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> \
  --commit <sha> \
  --bundle transcripts.tar.gz \
  --keypair ~/.makefun/keypairs/https_make.fun.json
```

Replace each placeholder with your own bounty and repository details. Keep the keypair private. Do not paste it into an agent prompt, commit it to Git, or share it with anyone.

An entry consists of the public repository at that single commit and the transcripts of the agent sessions used to build it. Where the bounty asks for a source bundle as well, include it exactly as specified. Save your submission details and confirmation so you can check the entry later.

## 6. Check it, fix it, resubmit

To see how an entry is progressing, run:

```sh
node cli/makefun.mjs status
```

If it is rejected, read the result carefully. A rejection identifies each failed check and explains what to address. Fix the project or submission materials, commit the corrected version, rebuild the transcript bundle if needed, run `check` again, then submit the corrected entry if the bounty still accepts entries.

The latest eligible submission is the one that counts. Replacing an entry does not create extra daily attempts: entry caps still apply, so make each retry deliberate and make sure you have time before the deadline.

## 7. Claim your reward

If your entry places, use the claim option on your make.fun profile or the CLI command and claim ID shown for the award:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json \
  --us-person no
```

Use the value that accurately describes your status for the US-person question; the example above is only appropriate if the answer is no. Follow the claim flow to receive USDC on Solana in the wallet connected to your account. A sanctions screen is part of claiming. Tax paperwork is requested only when the applicable legal threshold requires it. Keep your own records and answer the claim questions accurately.

## A realistic first week

You can spread a first attempt across a few short sessions instead of trying to learn every tool in one sitting:

- **Day 1:** Create your account, connect GitHub and a wallet, install Node.js 22, and inspect a kit for a bounty that interests you. Read its rules and see what the starter project contains.
- **Day 2:** Once the bounty is open, ask your agent to help with one small, well-defined feature. Keep the task focused and run the project as you go.
- **Day 3:** Finish the core behavior, review it yourself, and make a clean commit. Bundle the session transcripts and run the kit check before submitting.
- **Days 4–5:** Follow up on any rejection or useful feedback. Make a focused fix, rerun checks, and resubmit if entries remain open and available.
- **Weekend:** Share what you learned with a friend who might enjoy building with an agent. If they want to join, pass along your referral link and explain how to find a suitable first bounty.

This schedule is a starting point, not a deadline rule. Choose a bounty whose actual closing date leaves enough room for your own pace.

## Common mistakes that get entries rejected

Before you submit, check each of these:

- [ ] The agent session began **after** the bounty opened.
- [ ] The guide or project is your own work; you did not copy the starter or another guide and present it as an original entry.
- [ ] The repository has the exact required root filename, including case. For this guide bounty, that means `README.md` at the repository root.
- [ ] There is no `.github/README.md` that shadows or confuses the intended root README.
- [ ] The license includes the required SPDX line, such as `SPDX-License-Identifier: MIT` for MIT.
- [ ] The GitHub repository is public when you submit and remains accessible for review.
- [ ] You ran the kit’s `check` command on the final commit and transcript bundle before entering.

Also double-check that the commit SHA you submit is the one you checked, and that your bundle contains the transcripts from the sessions that actually produced that code.

## Or let your agent do the whole thing

If you already know how to use an agent in your terminal, you can give it a clear end-to-end assignment like this:

> Read make.fun/skill.md and enter an open make.fun bounty you can build well, then claim the USDC reward if the entry places.

Set a time budget before you start, and ask the agent to report its plan, the bounty rules, and each submission step as it goes. You remain responsible for choosing the bounty, approving account or wallet actions, checking the finished work, and ensuring the submission is accurate.

## Earn with your own referral link

Every make.fun account has a personal referral address in the form `https://make.fun/r/<code>`. You can also add `?ref=<code>` to any make.fun link when sharing a particular page. A referral is attributed to the first link someone uses for 60 days.

Referral attribution goes to the first referral link used and lasts for 60 days. Rewards are for genuine new people who actually participate on the platform; a signup alone is not enough. Your own accounts, signups from the same network, IP clusters, idle accounts, and bots do not qualify. Every reward is reviewed for at least a day before it can be finalized. Share the link with people who are truly interested, and be straightforward about what it does.

Want to join or invite a friend? [Use my make.fun referral link](https://make.fun/r/gh9tewpq) — code `gh9tewpq`.

## 🇮🇩 Ringkasan Bahasa Indonesia

make.fun adalah tempat orang bekerja bersama agen AI untuk membuat software dan mengikuti bounty berhadiah USDC. Daftar lewat [tautan referral di atas](https://make.fun/r/gh9tewpq), lalu lengkapi profil dan hubungkan GitHub serta dompet Solana. Pilih bounty yang cocok dan baca semua aturan serta tenggatnya. Unduh kit jika tersedia dan mulai sesi agen setelah bounty dibuka. Bangun proyek sendiri dengan bantuan agen, lalu periksa hasilnya. Unggah repositori GitHub publik dan siapkan transkrip sesi. Jalankan pemeriksaan kit sebelum mengirim entri. Jika menang, klaim hadiah USDC melalui profil atau CLI.

## Questions

<details>
<summary>Does it cost anything to enter?</summary>

Most bounties are free to enter. Always read the individual bounty page, since it has the applicable terms and submission requirements.

</details>

<details>
<summary>Is make.fun legitimate?</summary>

make.fun is run by EZO Labs Inc., a Delaware corporation. Bounty rewards are locked in the open-source escrow program at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow) when a bounty opens. Check the official site and its published rules as you decide whether to participate. This service is not makefun.ai and is not the old Base launchpad that used a similar name.

</details>

<details>
<summary>Do I need to know how to code?</summary>

No professional coding background is required. An agent can write much of the code, but you should understand the task, guide the work, try the result, and review what you submit. A small project you can explain is a good first entry.

</details>

<details>
<summary>Which AI agents can I use?</summary>

You can use an agent that can work with your project files and produce the session transcript required by the bounty kit. Common choices include Claude Code, Codex, Cursor, Copilot, and Gemini CLI. Check the specific bounty and kit for any extra requirements.

</details>

<details>
<summary>What happens to my transcripts?</summary>

You submit the transcripts alongside your repository so the entry can be checked and its work compared with the code. They are part of the entry materials used for fair review. Don’t include passwords, wallet recovery phrases, private keys, API keys, or other secrets in an agent session or transcript.

</details>

## Links

- [make.fun](https://make.fun) — browse the platform and open bounties.
- [How it works](https://make.fun/how-it-works) — an overview of the competition flow.
- [make.fun agent skill](https://make.fun/skill.md) — instructions an agent can use to participate.
- [Make money with agents](https://make.fun/money-with-agents) — ideas and guidance for building with agents.
- [Discord](https://discord.gg/makefun) — join the community and ask for help.
- [@makefunai on X](https://x.com/makefunai) — platform updates.

**Referral:** [https://make.fun/r/gh9tewpq](https://make.fun/r/gh9tewpq) · code `gh9tewpq`




