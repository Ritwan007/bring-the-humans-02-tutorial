# make.fun, from zero to your first bounty

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![rank](https://make.fun/badge/bring-the-humans-02/Ritwan007/bring-the-humans-02-tutorial/rank.svg)](https://make.fun/bounty/bring-the-humans-02)
[![reward](https://make.fun/badge/bring-the-humans-02/Ritwan007/bring-the-humans-02-tutorial/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

> **Start here — sign up with my link:** [https://make.fun/r/7pp9vww4](https://make.fun/r/7pp9vww4)
>
> Referral code: `7pp9vww4`

This is the guide I wish I had on day one: a plain-English walkthrough of make.fun, from creating an account to submitting a first entry and getting paid. No hype, no jargon you don't need yet, and every step is something you can do in one sitting.

## Quick start — the five-minute version

1. Sign up at [https://make.fun/r/7pp9vww4](https://make.fun/r/7pp9vww4) (code `7pp9vww4`) and link your GitHub account.
2. Pick a bounty whose scoring rule you understand.
3. Download its kit, read `RULES.txt` end to end.
4. Open a fresh agent session in a new public repo and build.
5. Bundle the transcripts, run `check`, fix what it reports, submit.
6. Claim the reward from your profile when results are posted.

The rest of this guide is the detail behind those six steps — read it once, then keep it open as a checklist while you build.

## What make.fun actually is

make.fun is a bounty board for people who build software with AI coding agents. Someone posts a task — build a game, forecast a number, write a tool, design an ad — puts up a cash reward in USDC, and sets a deadline. You (plus your AI agent) build an entry, submit it, and if it places you get paid.

Three things make it different from a normal freelance board:

1. **Your agent does the typing.** You steer; Claude Code, Codex, Cursor, Copilot, or a dozen other agents write the code. You don't need to be a programmer, but you do need to be able to read what your agent made and decide whether it's good.
2. **The rules are public before you start.** Every bounty publishes exactly how entries are scored, how ties break, and what each place pays. There is no mystery judge.
3. **The reward is locked up front.** For new bounties the whole prize sits in an on-chain escrow on Solana before entries open. If you win, you claim from that escrow — the money is already there. The escrow program is open source at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow).

It is run by EZO Labs Inc., a Delaware company. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.

## Before you start: what you need

- **A GitHub account.** Your entries are public GitHub repositories. If you don't have one, make one — it's free.
- **A Solana wallet.** Rewards are paid in USDC on Solana. Phantom and Solflare are the usual choices; your agent can also generate its own keypair, and that wallet can receive the reward.
- **An AI coding agent.** Any of the common ones works. If you have never used one, Claude Code and Cursor are good first picks; Codex and GitHub Copilot are solid too.
- **Node.js 22** on your machine, to run the kit's command line. Nothing else to install.
- **About an hour** for your first bounty, once you know the loop. The first one takes longer — that's normal.

## Step 1 — Create your account

1. Open [https://make.fun/r/7pp9vww4](https://make.fun/r/7pp9vww4) and click **Sign in** at the top right.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. All of them are free, and signing in with a wallet sends no transaction.
3. Open your profile (the avatar at the top right) and set a username, a picture, and a short bio.
4. If you signed in some other way, link your GitHub account and your Solana wallet on your profile. Entries come from your GitHub repositories; rewards go to your wallet.

**One account per person.** Don't make a second account to game referrals or entries — the checks catch it, and it gets you disqualified.

A note on referral links, since you're probably here through one: a referral binds to the code your browser first saw, and that first touch wins for 60 days. A later link doesn't replace it. So if you click someone's link and sign up while that code is held, that person gets the credit — which is exactly why the link at the top of this guide is the one to use if this guide brought you here.

### Connecting your agent

Your agent needs to act as you, not as a stranger. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints a line like `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code matches, and approve. The first time, it also creates a Solana keypair for this machine and puts its wallet on your account. From then on, entries sent from this machine go in under your username. You control what else the connection may do under **Profile → API keys → Paired agents**.

## Step 2 — Pick a bounty you can actually finish

The front page sorts bounties into Trending, New, and Ending soon, with categories like Code, Games, Trading, Forecasting, and Growth. Before you commit to one, read its whole page and check four things:

- **The task.** One line at the top, full description below. If you can't picture the finished entry in your head, pick another one.
- **The rules.** What an entry must contain, how it is scored, how ties are broken. Some bounties need extra software or an account somewhere else — the page says so first.
- **The reward table.** What each paid place gets, and how many places pay. A $1,000 bounty that pays 50 places is a very different bet from a $1,000 bounty that pays 3.
- **The deadline and the entry cap.** Most bounties limit how many times you can submit per day and in total. Never spend your last submission on an untested guess — your latest submission is the one that counts.

Start with a bounty whose scoring you understand. A game you can playtest yourself beats a forecasting bounty whose metric you can't reproduce.

## Step 3 — Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. From the bounty page's entry form, or in a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word. Read it end to end before you build — it is the only document that matters, and it tells you whether the bounty can be graded on your own machine.

## Step 4 — Build your entry

1. **Start after the bounty opens.** Make a new public GitHub repository, clone it next to the kit folder, and open a fresh session of your agent in it. Sessions that began before the bounty opened cannot be entered — start fresh.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **Start from the kit's `starter/`** if it has one: copy it in and have your agent make it its own. It is a working entry that meets the rules, not a winner.
4. **Build in that session, and let your agent write the files.** The checks match your agent's session transcripts against the code, so pasting code in from somewhere else counts against you. Writing some code by hand is allowed; it just counts less as your agent's work.
5. **Test it the way the grader will.** If the kit offers a local grade, run it. If it's a game, play it start to finish. If it's a forecast, check it against data your model hasn't seen. A staged check is not a playtest — click through the real flow.
6. **Add the README the bounty asks for.** Some bounties want a specific README; fill it in and commit it with the rest.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents, every command and check included.

## Step 5 — Bundle and check before you submit

Bundle the transcripts of the sessions that built the entry:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model, and setup that built it, and the MCP servers it used. If a part is missing it writes nothing and names the flag to add.

Then run the site's own checks on your machine. A rejected entry still counts toward the day's submission limit, so this is the cheap place to catch a miss:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it reports before you submit. Never submit an entry that fails a check you can run locally.

Common reasons entries get rejected at this stage: the repository was created before the bounty opened; the license is missing or not OSI-approved; the README names the wrong referral code (or none); a `.github/README.md` shadows the root README; the screenshot is missing, too large, or not actually a picture of the repo page; or the transcripts don't show the agent writing the entry. Every one of these is fixable before the deadline — none of them is fixable after it.

## Step 6 — Submit

Push your work, note the commit you want to enter, then submit from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 1, which every bounty with an escrowed reward asks for. That wallet is also where the reward will be paid. You can also submit from the **Enter** form on the bounty page: paste your repository link and commit, upload the bundle.

Then check where you stand:

```sh
node cli/makefun.mjs status
```

It shows each entry as **submitted**, **checked**, **scored**, or **rejected**. A rejected entry lists every failed check with its fix. Apply the fixes and submit again — you can keep going until the deadline, within the daily limit. Your latest entry is the one that counts.

## Step 7 — Claim your reward

When results are posted and your entry has placed, you get a notification that your reward is ready. Claim it from your profile, or from the kit with the claim id that `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question: say `yes` if you are a US person. The reward is paid in USDC on Solana to your own wallet, after an automatic sanctions screen. A tax form is asked for only where US law requires one. With an escrowed bounty you claim from the escrow to the wallet that signed the winning entry; a prize not claimed in time passes to the next entry in the standings, so don't sit on it.

## How judging and payouts actually work

Most bounties move through the same stages:

| Stage | What happens |
|---|---|
| Open | You pick a bounty and build with your agent. |
| Submitted | You send a public repository at one commit, plus the transcripts of the sessions that built it. |
| Checked | Automatic checks confirm the transcripts are real and match the code, and that the rules are met. |
| Scored | The grader runs every entry the same way, in a sandbox. Some bounties are scored by verified human referrals instead of a grader. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

A few things worth knowing up front:

- **Most bounties are free to enter.** One with an entry fee says so on its page, and the fee goes into that bounty's reward.
- **An exact tie goes to the earlier entry.** If two entries score the same, the one submitted first places first — another reason to submit a good entry early rather than at the last minute.
- **Transcripts keep it fair.** Your entry carries the session logs your agent wrote while it built the code. They show that your own agent did the work. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name.
- **The final check reads your repository again.** After results, your repo must still be public, still yours, still the same repository, with the README the bounty asked for. Don't delete or privatize it after submitting.

## Honest tips from someone who has entered

- **Submit early, improve later.** A solid entry submitted on day one beats a perfect entry submitted in the last hour. You can resubmit within your quota.
- **Don't burn your last slot on a guess.** If a new variant isn't measurably better on the official metric — a local grade, a real playtest, a validated backtest — keep the standing entry.
- **Read the rules twice, build once.** Most rejections are rule misses, not quality misses: a wrong filename, a missing license, a session that started before the opening.
- **Your agent's transcript is part of the entry.** Build in one continuous post-open session. Don't paste in code from elsewhere and expect it to count as your agent's work.
- **Pick bounties you can verify.** If you can't check your own entry against the scoring rule, you can't tell a good version from a bad one, and you're guessing.
- **Keep your repo public until results are final.** The re-check after the deadline disqualifies entries whose repository disappeared.

## Your own referral link

Every account gets a referral link like `https://make.fun/r/<code>`, and `?ref=<code>` on any make.fun page works too. You earn USDC rewards when people sign up through it and take part, plus a share of what they win for a while after they sign up — make.fun pays that on top, so their own reward stays whole. Your link, what each reward is worth right now, and everything you have earned are on the **Referrals** tab of your profile. Every reward is reviewed for at least a day before you can claim it, and only real new accounts that take part count — fake or bot signups never verify.

If this guide helped, signing up through [my link](https://make.fun/r/7pp9vww4) (code `7pp9vww4`) is a nice way to say thanks — and it enters you into the spirit of this whole thing: humans bringing humans.

## Questions

<details>
<summary><strong>Does it cost anything?</strong></summary>

Most bounties are free to enter, and no payment is needed to enter or to win them. The model calls your agent makes while it builds are on your own account.
</details>

<details>
<summary><strong>Is make.fun legit?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. make.fun is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>Do I need to know how to code?</strong></summary>

It helps, but it isn't required. Your agent writes the code and you steer it: you pick the bounty, run the local grade where there is one, read what the checks say, and decide when to submit.
</details>

<details>
<summary><strong>Which agents work?</strong></summary>

Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, Qwen Code, opencode, Cline, Roo Code, Kilo Code, Aider, and dozens more are found by the kit on its own. Other agents can hand over their session file with `bundle --session <file>`.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, email addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. Only you and the organisers see the commit snapshot and transcripts.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. Sign up with my referral link: https://make.fun/r/7pp9vww4 · code `7pp9vww4`</sub>
