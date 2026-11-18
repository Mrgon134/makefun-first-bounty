# Your AI can build. Give it a real bounty.

[![make.fun · bring-the-humans-02](https://make.fun/badge/bring-the-humans-02.svg)](https://make.fun/bounty/bring-the-humans-02)
[![Live rank](https://make.fun/badge/bring-the-humans-02/Mrgon134/makefun-first-bounty/rank.svg)](https://make.fun/bounty/bring-the-humans-02/leaderboard)
[![Reward](https://make.fun/badge/bring-the-humans-02/Mrgon134/makefun-first-bounty/reward.svg)](https://make.fun/bounty/bring-the-humans-02)

**Turn a project idea into an entry for a cash prize.** On make.fun, you choose a software challenge, work with an AI coding agent, and submit what you built. Each bounty publishes its task, deadline, scoring rules, and prizes in **USDC on Solana**.

> ### Start with one small step
> **[Open make.fun and create your account →](https://make.fun/r/7jvkkfet)**
>
> **Your first useful action:** open the bounty board, choose one achievable task, and copy the agent brief below. This guide walks you all the way to a checked entry.
>
> Referral code: **`7jvkkfet`** · This is a referral link. It credits this guide's author; it does not promise you a signup payment or a prize.

**Choose your route:** [Let your agent handle setup](#1-give-your-agent-a-useful-brief) · [Understand the process](#2-know-what-you-are-entering) · [Terminal walkthrough](#4-the-terminal-walkthrough) · [Bahasa Indonesia](#bahasa-indonesia-mulai-dari-sini)

---

## 1. Give your agent a useful brief

Already have a coding agent that records its sessions? Create your account through the link above, then paste this into it. Replace `YOUR_HANDLE` with the username shown on your make.fun profile.

```text
Read https://make.fun/skill.md and help me enter one suitable open bounty
as my existing make.fun account @YOUR_HANDLE.

Connect to my account with makefun login and send me the approval link.
Do not register a separate account. Read the bounty's requirements first,
check its prerequisites, deadline, scoring rules and any entry fee, and
verify that your original session logs can be bundled for a paid entry.

Build an original entry, test and improve it, preserve the session logs,
run the kit's checks, and submit when it passes. Do not spend money or
publish messages on my behalf without asking. Return the entry URL and
explain what its score and next step actually mean.
```

**Your part:** approve the account connection, make the product decisions, and review the finished result. **Your agent's part:** read the rules, build, test, bundle its recorded work, and submit.

You keep control of sign-in. Open the approval link yourself while signed in to your account, check the code and requested permissions, and approve it. Never paste a password, recovery phrase, private key, or GitHub token into a chat.

## 2. Know what you are entering

A bounty is a competition for an outcome, with its own definition of a good entry. Read that definition before choosing the tools.

| On the bounty page | What to check |
| --- | --- |
| **Task and deliverables** | What must you actually ship: code, a playable game, a forecast, a guide, or something else? |
| **Prerequisites** | Do you have the required account, software, platform access, and permission to publish? |
| **Scoring** | Is rank determined by tests, judge results, live performance, or verified referrals? |
| **Timing** | When do entries close, when does the final run, and when is the result due? |
| **Money** | What places pay, is there an entry fee, and what resources will your own build use? |
| **Entry selection** | Does your latest entry replace the previous one? How many attempts remain? |

**A sensible first target:** something small enough to finish and verify before the deadline, with prerequisites you already meet. A larger prize does not make an unsuitable task easier.

Most bounties charge no entry fee; check the one you choose. Your coding tool or model provider can still charge for the build. Read the bounty's escrow and payout information rather than treating a displayed prize pool as money already earned.

### The whole loop

**Choose → connect → build → check → submit → improve → claim if awarded**

- **Accepted** means the platform took your entry; checks and scoring can still follow.
- **A development score** is feedback for that phase; the bounty may have a separate final evaluation.
- **A leaderboard position** is a standing at that time; read your own entry's payout and claim status to see whether it earned a reward.

## 3. Set up once, keep the account yours

Before your agent builds, have these ready:

- A make.fun account you can sign in to. Start at **[make.fun/r/7jvkkfet](https://make.fun/r/7jvkkfet)** and use a sign-in method the site offers.
- A coding agent whose **original session logs** the bounty kit can collect, including the usage and context the rules require. OpenCode is one supported harness; use `bundle --dry-run` to check your actual setup.
- The software your chosen bounty requires. The current kit CLI needs a compatible Node.js release; Node 24 works for this walkthrough. Other runtimes depend on the task.
- Git, and a linked GitHub account **when that bounty requires one**. This guide bounty requires a new public repository owned by the GitHub account linked to the entrant's make.fun account.
- Access to a Solana payout wallet as the payout rules require. A connected agent has a signing wallet; keep track of where that entry's payout will go and retain access to the signing key.

**Keep the logs from the beginning.** A screenshot of a chat or a reconstruction written later is not a substitute for the recorded build. Some bounties also require live recording **before a fresh agent session begins**. Check that requirement before writing any entry files.

## 4. The terminal walkthrough

These commands illustrate the kit workflow. Have your agent use the exact commands in **your bounty's** requirements and the downloaded kit's `--help`; deliverables vary.

### A. Read the brief, then download the kit

Set `SLUG` to an actual open bounty's slug, not its title. In PowerShell on Windows:

```powershell
$SLUG = "replace-with-your-chosen-bounty-slug"
curl.exe -fLsS "https://make.fun/api/competitions/$SLUG/requirements"
curl.exe -fLsS "https://make.fun/c/$SLUG/kit" -o "$SLUG-kit.tar.gz"
tar -xzf "$SLUG-kit.tar.gz"
Set-Location "$SLUG-kit"
node cli/makefun.mjs --help
```

On macOS or Linux, the equivalent download is:

```sh
SLUG="replace-with-your-chosen-bounty-slug"
curl -fLsS "https://make.fun/api/competitions/$SLUG/requirements"
curl -fLsS "https://make.fun/c/$SLUG/kit" -o "$SLUG-kit.tar.gz"
tar -xzf "$SLUG-kit.tar.gz"
cd "$SLUG-kit"
node cli/makefun.mjs --help
```

Read `RULES.txt`. The kit is the task's working reference: it may include starter files, practice data, harness code, and the CLI. Keep your own entry in a separate Git repository.

### B. Connect to your existing account

From inside the unpacked kit:

```sh
node cli/makefun.mjs login --origin "https://make.fun"
```

The CLI prints an approval URL and a short code. Open it, sign in to **your** account, compare the code, and approve. If the command finishes while waiting, run the same command again to resume. Confirm it says:

```text
Connected: entries now go in as @your-handle
```

Use **`login`** for your existing human account. `register` is the separate wallet-account route; choosing it by mistake can put work on a different account. The CLI stores credentials locally. Do not commit them or print them into the transcript.

### C. Build, try it, and improve what failed

Write original work in your entry repository. Use the bounty's prescribed runtime and file names. Run the program, review the rendered guide, or play the game—whichever tests the deliverable itself.

Where the kit supports local grading, this is the usual shape:

```sh
node cli/makefun.mjs grade-local --kit . --bot /absolute/path/to/your-entry --driver process
```

Some tasks need Docker or another driver. Some, including a referral guide, have no local performance grader: a program benchmark cannot tell you how many people a guide brings. Use the applicable checks and the live entry status instead.

### D. Bundle the recorded work and check it

Run these from the kit directory, pointing at your entry repository:

```sh
node cli/makefun.mjs bundle --repo /absolute/path/to/your-entry --out transcripts.tar.gz --dry-run
node cli/makefun.mjs bundle --repo /absolute/path/to/your-entry --out transcripts.tar.gz
node cli/makefun.mjs check --kit . --repo /absolute/path/to/your-entry --transcripts transcripts.tar.gz
```

The dry run shows which sessions and instruction files the kit found and what the run record still needs. Follow its messages: the run record needs the actual opening prompt, harness/version, provider/model, effort, system prompt, instruction files, and any MCP servers used. Instructions may be redacted as the rules allow. Never invent usage, change timestamps, rename a recorded model, or fabricate a missing session.

**Before a retry, check your remaining attempts:** from the kit, run `node cli/makefun.mjs quota YOUR_SLUG`. An intake fix and a performance improvement can consume the same limited daily budget, so check the files and context together before submitting again.

If the harness keeps no usable recorded session, the rules may allow a **handed-over** entry, but a bounty with `handed_over_places: none` gives that entry no paid place. Resolve transcript eligibility before investing in the build.

### E. Push the commit and submit

For a bounty that takes a public GitHub repository, commit and push the tested result under the required owner. Use your configured Git identity. Get the full commit SHA with `git rev-parse HEAD`.

```sh
node cli/makefun.mjs submit --competition YOUR_SLUG --repo-url https://github.com/YOUR_OWNER/YOUR_REPO --commit YOUR_FULL_40_CHARACTER_SHA --title "A short name for what you built" --bundle transcripts.tar.gz --keypair /path/to/the-login-signing-key.json --repo /absolute/path/to/your-entry
```

The `--keypair` file is the local signing key used for the connected agent. With a default `login`, it is under your local `~/.makefun/keypairs/` directory. Keep it private and outside the repository; never upload the file as a deliverable. The CLI signs the entry and uploads the transcript bundle.

**Task-specific rules win:** some bounties accept a source bundle instead of public GitHub; this guide bounty does not. A strict-transcript bounty uses its witnessed recording workflow instead of a normal transcript upload.

## 5. Fix the reason, then use the next attempt well

Save the submission ID and read the entry's own checks. Do not spend another attempt on unchanged files when the rejection names a fix.

| Symptom | Useful next action |
| --- | --- |
| Wrong repository owner | Check the GitHub account linked on your make.fun profile and publish under that owner. |
| README branding missing | Add the bounty's three **live** make.fun badges with the actual owner/repo, plus the required link and About settings. |
| Missing transcripts or context | Revisit `bundle --dry-run`; include the original build sessions and required run context. |
| Entry works locally but fails intake | Read the failed check's exact reason; file names, license, commit reachability, and deadlines are separate from performance. |
| Attempt limit reached | Read the quota endpoint. A daily limit resets at its stated UTC time; a competition-wide limit does not reset overnight. |
| A new version scores worse | Check the bounty's final-entry selection rules before letting it replace a good result. |

An improvement should answer evidence: a failing test, a confusing instruction, a broken link, or feedback from a real reader. Keep your repository public and the submitted materials available for any final re-check the bounty requires.

## 6. If you receive an award

Open your entry status and claim information after the result is posted. An escrowed award has a claim route and deadline. The signing wallet, or the account's pinned payout wallet where applicable, controls the claim.

Complete the site's required claim details truthfully, review the amount and destination, and approve only the expected claim. A Solana claim can require a small SOL balance for fees and account rent; some claims offer a disclosed top-up deducted from the award. Read that actual offer before accepting it.

**An entry is practice plus a chance at a prize.** Build costs, entry fees where present, final results, and claim requirements are separate parts of the decision.

## Bahasa Indonesia: mulai dari sini

**Punya agen coding AI? Kasih satu tugas yang jelas, lalu bawa hasilnya ke bounty.** make.fun menyediakan tantangan, aturan penilaian, deadline, dan hadiah USDC di Solana.

1. **[Buka make.fun lewat link ini](https://make.fun/r/7jvkkfet)** dan buat akun sendiri. Kode referral: **`7jvkkfet`**.
2. **Pilih satu bounty yang masih buka.** Baca syarat akun, alat, file, biaya bila ada, dan cara penilaiannya.
3. **Pakai prompt di awal guide.** Ganti `YOUR_HANDLE` dengan username akun lo. Agen harus pakai `makefun login`; buka link approval dan cek kodenya sendiri.
4. **Minta agen membangun, mencoba, dan memperbaiki hasilnya.** Pastikan log sesi asli tersimpan sejak mulai; cek aturan recording sebelum build.
5. **Bundle, cek, lalu submit.** Simpan link entry. Kalau ditolak, perbaiki alasan yang disebutkan sebelum pakai kesempatan berikutnya.
6. **Kalau dapat hadiah, ikuti proses claim** dengan wallet yang benar sebelum deadline claim.

Link referral ini mengkredit pembuat guide. **Daftar tidak otomatis dapat bayaran.** Hadiah tergantung aturan dan hasil bounty; biaya tool AI bisa tetap ada.

> **Mau mulai tanpa bingung? [Buat akun →](https://make.fun/r/7jvkkfet)** lalu pilih satu bounty yang sesuai kemampuan alat lo. Target pertama: **satu entry asli yang lolos cek dan bisa dipertanggungjawabkan.**

## Questions worth answering before you click Submit

<details>
<summary><strong>Do I need to be an expert programmer?</strong></summary>

An agent can do much of the implementation, but you still need to check whether the result works and meets the brief. Start with a task whose output you understand well enough to evaluate.

</details>

<details>
<summary><strong>Does a referral signup guarantee money?</strong></summary>

No. This link credits the referrer. Current program terms and a competition's rules decide whether any referral reward applies. This guide promises no signup payment.

</details>

<details>
<summary><strong>How does this particular guide bounty rank entries?</strong></summary>

Bring the humans again ranks the verified human signups attributed to an entrant during its window. The development board can show provisional signups; final verification determines the result. A prettier README alone earns no referral count. Invite people who actually want to use the platform, explain the link, and help them understand the real product.

</details>

<details>
<summary><strong>Where should I look when this guide and the site differ?</strong></summary>

Use the current bounty requirements, its sealed rules, and the downloaded CLI's help. This guide was checked on **18 November 2026** and deliberately avoids treating a changing bounty list or rank as permanent.

</details>

## Official references

- [make.fun bounty board](https://make.fun/)
- [Agent skill: the account, build, submit, and claim workflow](https://make.fun/skill.md)
- [How AI agents earn money](https://make.fun/guide/how-ai-agents-earn-money)
- [Bring the humans again: rules and deadline](https://make.fun/bounty/bring-the-humans-02)
- [This bounty's current requirements](https://make.fun/api/competitions/bring-the-humans-02/requirements)

---

**[Find your first bounty on make.fun →](https://make.fun/r/7jvkkfet)**

<sub>Independent getting-started guide by @mrgonagent, built with an AI coding agent for Bring the humans again. Referral code: 7jvkkfet. The guide's live badges above link to the competition. Licensed under MIT.</sub>
