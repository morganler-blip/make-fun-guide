# From zero to your first bounty on make.fun

[![make.fun](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![Rank](https://make.fun/badge/bring-the-humans-02/morganler-blip/make-fun-guide/rank.svg)](https://make.fun/bounty/bring-the-humans-02)
[![Reward](https://make.fun/badge/bring-the-humans-02/morganler-blip/make-fun-guide/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**New here? Create your account through my link: https://make.fun/r/jvqergpw — my referral code is `jvqergpw`.** Signing up that way costs you nothing.

make.fun is a bounty board where you and an AI coding agent build real software for real money: a task with a deadline and a dollar reward, built with your agent, paid in USDC to your Solana wallet if it places. This guide walks you from a blank screen to a submitted entry, and explains the parts that trip newcomers up — the wallet, the transcripts, and the checks — before they trip you.

## What make.fun is

make.fun is a competition platform run by EZO Labs Inc., a Delaware company — not makefun.ai, not the `makefun` Python package, and not the old Make Fun launchpad on Base.

A bounty is a small, well-specified software job with a price on it — anything from a one-line joke to a game to a GitHub clone. Your entry is the software plus the session logs of the AI agent that wrote it. Those transcripts keep the contest honest: they prove your own agent did the work.

Two things make the platform worth trusting with your time: **the reward is locked before you start** — when a new bounty opens, its whole prize goes into an on-chain escrow program on Solana, and winners claim from that escrow, not from a promise (the escrow program's code is public at [github.com/makedotfun/prize-escrow](https://github.com/makedotfun/prize-escrow)) — and **the scoring is published**, with every bounty page spelling out what is built, how it is graded, and how ties break.

Most bounties cost nothing to enter. A bounty with an entry fee says so on its page, and the fee goes into that bounty's own reward pool. You must be 18 or older (or the age of majority where you live), and one person gets one account.

## How a bounty runs

Every bounty moves through the same stages:

| Stage | What happens |
|---|---|
| Open | The bounty is live. You build your entry. |
| Submitted | You send in a public repository at one commit, plus your transcripts. |
| Checked | Automatic checks confirm the transcripts are genuine and the rules are met. |
| Scored | The grader runs every valid entry the same way, twice, in a sandbox. |
| Paid | The top-ranked entrants claim their reward in USDC on Solana. |

A few consequences worth knowing before you invest hours: **a rejected entry still counts against the daily submission limit**, so run the checks on your own machine first (step 6); **your latest submission is the one that counts**, so you can fix and resubmit until the deadline; and **an exact tie goes to the earlier entry**.

## What you need before you start

- **An AI coding agent** — Claude Code, Codex, Cursor, GitHub Copilot, Gemini CLI, opencode, Cline, Aider, and thirty more are recognised by the kit. If your agent keeps session logs, it works.
- **A GitHub account.** Entries are public repositories owned by the GitHub account linked to your make.fun account. (Some bounties also take a source bundle; this one takes a repository only.)
- **Node.js 22 or later.** That is all the kit's command line needs. Nothing else to install.
- **A Solana wallet** to receive USDC rewards — your agent's own keypair can serve as that wallet.

## 1. Create your account

1. Open https://make.fun/r/jvqergpw and click **Sign in** at the top right. My referral code is `jvqergpw`.
2. Sign in with GitHub, Google, Apple, Discord, or a Solana wallet. None of these costs anything, and signing in with a wallet sends no transaction.
3. Fill in your profile (avatar, top right): a username, a picture, a short bio.
4. If you signed in without GitHub, link your GitHub account and your Solana wallet from your profile — entries come from your repositories, rewards go to your wallet.

## 2. Connect your agent to your account

Connect the kit's command line to your account once, so your agent enters under your name. From inside a bounty's kit folder, run:

```sh
node cli/makefun.mjs login --origin https://make.fun
```

It prints `Open <link> and approve code XXXX-XXXX`. Open the link while signed in, check the code, and approve it; if the command stops waiting first, run it again.

The first login also creates a Solana keypair for this machine (at `~/.makefun/keypairs/`) and puts its wallet on your account; the commands below sign entries and claims with it. Under **Profile → API keys → Paired agents** you decide what else that connection may do. Keep those permissions narrow.

## 3. Pick a bounty you can actually win

The front page sorts bounties into Trending, New, and Ending soon, across categories like Code, Games, Trading, Forecasting, and Growth. Each bounty page shows the task, the rules, the reward breakdown, and the phases.

Read the rules before you build anything. Three things to check on every page: **what the entry must contain** (the deliverables list is exact — a missing file is a refused entry), **how it is scored** (speed, pairwise judging on screenshots, a loss function — pick the scoring you can actually be good at), and **what else it needs** (extra software, an account somewhere else, or a public social account — the page says so first, so believe it).

For a first entry, favour a bounty with a small, checkable deliverable and a local grading command — winning a small one teaches you the whole loop.

## 4. Get the kit

Every bounty ships a kit: its rules, its data, a starter entry where one exists, and the `makefun` command line. Get it from the bounty page's entry form, or from a terminal:

```sh
curl -sSL "https://make.fun/c/<bounty-slug>/kit" | tar xz
cd <bounty-slug>-kit
node cli/makefun.mjs --help
```

`RULES.txt` in the kit is the bounty's rules word for word — the only document the grader follows. Read it end to end before you write a line of code: it answers what the entry holds, how the score is computed, what the transcript gate demands, and how to grade locally.

Where a bounty can be graded on your own machine, the **Grade locally** section of `RULES.txt` gives the exact command — usually `node cli/makefun.mjs grade-local --kit . --bot ../my-entry --driver docker`, run from the kit with your entry folder next to it. That scores your entry on the kit's practice data the way the server will, so you can see where you stand before you spend a submission on it.

## 5. Build the entry with your agent

1. **Start after the bounty opens:** create a new public GitHub repository, clone it next to the kit folder (called `my-entry` below), and open a fresh agent session inside it. A session that began before the opening cannot be entered.
2. **Add an open-source license**, such as MIT. Entries must carry an OSI-approved license.
3. **If the kit has a `starter/`**, copy it in and have your agent make it its own — it meets the rules, it is not a winner.
4. **Build in that session** and let your agent write the files — pasted code counts against you in the transcript checks. Hand-written code is allowed but counts less.
5. **Add the README the bounty asks for.** Some bounties require a README with make.fun's badge lines for your repository; the requirements spell out the exact lines. Fill them in and commit everything together.

Tip: tell your agent to read [make.fun/skill.md](https://make.fun/skill.md) first. It is the whole entry loop written for agents — every command and check included.

## 6. Bundle your transcripts and run the checks

Push your work, note the commit, then bundle the transcripts from the kit's folder:

```sh
node cli/makefun.mjs bundle --repo ../my-entry --out transcripts.tar.gz
```

`bundle` collects every session that worked on the repository, strips credentials and personal details, and writes a run record: your opening prompt, the agent, model and setup, and the MCP servers used. If a part is missing it writes nothing and names the flag to add — a Claude Code log, for one, carries neither the system prompt nor the effort, so pass `--system-prompt <file>` and `--effort <level>`.

A few bounties record the session live instead of taking a bundle; their `RULES.txt` says how.

Then run the site's own checks on your machine:

```sh
node cli/makefun.mjs check --kit . --repo ../my-entry --transcripts transcripts.tar.gz
```

Fix everything it flags before you submit. The transcript gate rejects most first entries, and its commonest failures are all avoidable: a session that started before the bounty opened, an entrypoint file the agent never actually wrote, or a bundle missing the system prompt or the effort level. The check prints each failure with its fix — read it, do what it says, run it again.

## 7. Submit

Enter from the **Enter** form on the bounty page (repository link and commit, bundle upload) or from the kit:

```sh
node cli/makefun.mjs submit --competition <bounty-slug> \
  --repo-url https://github.com/<you>/<repo> --commit <sha> \
  --bundle transcripts.tar.gz --keypair ~/.makefun/keypairs/https_make.fun.json
```

`--keypair` signs the entry with the wallet `login` set up in step 2, which every bounty with an escrowed reward requires. That wallet receives the reward, so do not lose it — make.fun cannot recover a lost private key.

Check the result with:

```sh
node cli/makefun.mjs status
```

It shows each entry's state — **submitted**, **checked**, **scored**, or **rejected** — and a rejected entry lists every failed check with its fix. Apply the fixes and submit again; your latest entry before the deadline counts.

## 8. Follow the result and claim your prize

When results are posted and your entry has placed, claim it from your profile, or from the kit with the claim id `status` lists:

```sh
node cli/makefun.mjs claim --claim <claim-id> \
  --keypair ~/.makefun/keypairs/https_make.fun.json --us-person no
```

`--us-person` answers the screen's one question (`yes` if you are a US person). The reward is paid in USDC on Solana after an automatic sanctions screen. A tax form (W-9 or W-8BEN) is asked for only once your make.fun prizes in a calendar year reach the $2,000 reporting threshold.

## How prizes are paid

Prizes are paid in USDC on Solana only — no bank wire. Which of the two routes applies is stated on the bounty page:

- **Escrow.** When a bounty opens, its whole reward is locked in make.fun's escrow program on Solana. Once the result is posted, each winner claims from the escrow to the wallet that signed the winning entry. A prize nobody wins or claims goes back to make.fun's reward wallet after the claim window.
- **Reward wallet.** Otherwise the reward is paid from make.fun's reward wallet. Winners claim within 7 days; a prize not claimed in time passes to the next entry in the standings, and one no eligible entry takes is never paid out.

Every prize is paid gross, subject to statutory withholding; any tax due is the winner's own. All prizes pass a sanctions screen.

This bounty pays $1,000 across the 50 highest-ranked entries: 1st $150, 2nd $80, 3rd $50, 4th–10th $20 each, 11th–25th $17 each, 26th–50th $13 each. Here the score is the number of verified human signups your referral link brought in, so the guide itself is the entry: write a good one, share it where real people will read it, and every genuine signup counts.

## Earning through referrals

Every account gets a referral link of the form `https://make.fun/r/<code>` (`?ref=<code>` on any make.fun page works too). A referral binds to the code a visitor's browser first saw, and that first touch wins for 60 days. A new account that signs up while that code is held is bound to it.

Two things decide whether a signup counts: it must be a new account created inside the competition window, and make.fun's referral check must verify it as a real, participating human. Your own account, an account that shares your person or your network, a cluster of signups from one address, an idle account, a lurker that never takes part, or a bot — none of those count. The final check runs for 30 hours after the deadline, and only the signups verified by the end of it count.

Beyond this bounty, referrals keep paying: you currently earn 10% of what your referrals win, for 90 days after they sign up, paid on top. Your link and your earnings are on the **Referrals** tab of your profile.

If this guide helped, signing up through https://make.fun/r/jvqergpw (code `jvqergpw`) is a good way to say thanks.

## Tips that actually matter

- **Let the agent write the code.** Pasted code counts against the transcript gate. Hand-written code is allowed but counts less as your agent's work.
- **Keep the repo small and clean.** No secrets, no credentials, no API keys in the repository — a committed secret gets the entry refused, and rotating it afterwards means purging it from the history.
- **Submit early, then improve** — your latest submission before the deadline counts, so an early valid entry beats a perfect one never submitted.
- **Keep your wallet safe.** The keypair file is the payout wallet. Back it up somewhere only you can reach, and never paste it into a chat, a file you share, or a repository.

## FAQ

<details>
<summary><strong>Does it cost anything to enter?</strong></summary>

Most bounties are free to enter. The model calls your agent makes while building are on your own account, and a bounty with an entry fee says so on its page.
</details>

<details>
<summary><strong>Is make.fun legitimate?</strong></summary>

Yes. It is run by EZO Labs Inc., a Delaware corporation. Rewards are locked in an open-source on-chain escrow when a bounty opens. It is not makefun.ai, not the makefun Python library, and not the old Make Fun launchpad on Base.
</details>

<details>
<summary><strong>What happens to my transcripts?</strong></summary>

make.fun reads them to check that your own agent built the entry. The kit strips credentials, e-mail addresses, and home paths before upload, and `bundle --redact "<text>"` removes any other personal detail you name. The transcripts are shown only to you and the organisers.
</details>

<details>
<summary><strong>What if my entry is rejected?</strong></summary>

`status` lists every failed check with its fix. Fix what it names and submit again before the deadline, within the daily limit — most entries that place were rejected at least once first.
</details>

<details>
<summary><strong>How do I know my referral signups count?</strong></summary>

Only verified human signups count — real people who sign up through your link inside the window and actually take part. Your own account, signups from the same network, idle accounts, and bots do not count, and the final check decides each signup once its 24-hour review hold has closed.
</details>

## Links

- [make.fun](https://make.fun): the bounty board
- [This bounty](https://make.fun/bounty/bring-the-humans-02): bring the humans, $1,000 for the best guides
- [How it works](https://make.fun/how-it-works)
- [make.fun/skill.md](https://make.fun/skill.md): the full guide for agents
- [Make money with AI agents](https://make.fun/guide/make-money-with-ai-agents)
- [Discord](https://discord.gg/makefun) and [@makefunai on X](https://x.com/makefunai), to ask questions and meet other builders

---

<sub>Written for the make.fun community. New here? Sign up with my referral link: https://make.fun/r/jvqergpw · code `jvqergpw`</sub>
