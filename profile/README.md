<p align="center">
  <a href="https://selflabs.org">
    <img src="https://selflabs.org/og.png" width="680" alt="Self-Labs">
  </a>
</p>

<p align="center"><strong>A one person lab, with uptime.</strong></p>

<p align="center">
  <img src="https://img.shields.io/badge/commits-1408-0b2a2f?style=flat-square&labelColor=0b2a2f&color=22d3ee" alt="commits">
  <img src="https://img.shields.io/badge/repositories-29-0b2a2f?style=flat-square&labelColor=0b2a2f&color=22d3ee" alt="repositories">
  <img src="https://img.shields.io/badge/upstream_PRs-13-0b2a2f?style=flat-square&labelColor=0b2a2f&color=34d399" alt="upstream PRs">
  <img src="https://img.shields.io/badge/running_since-Jul_2025-0b2a2f?style=flat-square&labelColor=0b2a2f&color=34d399" alt="running since July 2025">
</p>

<p align="center">
  <sub>Counted from the GitHub API on 2026-08-24, not estimated. The live figures update themselves every Monday at <a href="https://selflabs.org">selflabs.org</a>.</sub>
</p>

---

## The "self" is literal

Self-hosted, self-custody, done by hand. No managed database without a reason,
no deploy that depends on someone logging into a server, no private key inside a
machine that talks to the internet.

What lives here is software that already broke in production, was fixed, and
kept running. Signed firmware for a Bitcoin hardware wallet. A store that erases
the buyer's personal data 72 hours after delivery. A personnel system with
around 500 military police officers inside. Docker images that rebuild
themselves every Sunday and burn no runner minutes when nothing changed.

When something went wrong, it is written in the repository that it went wrong,
with a date and a file reference. That is traceability, not modesty.

## In production

| | What it is |
|---|---|
| **Wallet Store** | Bitcoin only store. Watch only xpub, every address derived locally, buyer data destroyed 72h after delivery by a scheduled command. |
| **ALFERES** | Personnel, leave, headcount and health for a military police unit. Administering and commanding are two axes that never mix, and the scope is enforced in SQL with a recursive CTE over the chain of command, not on the screen. |
| **Jade DIY** | Off the shelf ESP32 boards turned into a working Blockstream Jade. Signed firmware, web flasher, battery and touch logic for four boards. |
| **Escala e Folgas** | Shift and leave scheduling. Authorization lives in the token's `app_metadata`, because `user_metadata` is writable by the user. |
| **Atlas Logistics** | Fleet and delivery routing. |
| **Crypto Tracker** | On chain balance read from a pool of three Electrum servers, with a three source price cascade behind a circuit breaker. |
| **Portal Cativo** | Voucher authentication for OpenWrt routers. The uplink monitor only declares the internet down when three independent targets fail, and waits three cycles before waking the admin, because a network hiccup is not an outage. |
| **[selflabs.org](https://selflabs.org)** | This lab's landing page. Astro, bilingual, Cloudflare Workers, numbers pulled from the GitHub API instead of typed. |

Most repositories here are private, because they carry production systems for
real organizations. The public write up of each one, with what broke included,
is at **[selflabs.org](https://selflabs.org)**.

## Five things that repeat in every project

Not wall principles. Each one shows up in the code of at least three projects.

1. **GitOps with no manual step, on owned hardware.** Push to `master`, CI tests
   and builds, the Portainer webhook redeploys. The deploy job fails loud on any
   HTTP status outside 2xx. ARM64 builds run on a native runner, never under
   emulation, because the target is an Orange Pi 5 or an Ampere VPS.
2. **Verification instead of trust.** A check runs at the entrypoint, before the
   app server, and refuses to boot if the configured keys derive an address
   other than the expected one. A swapped xpub does not silently become a
   redirected payment.
3. **Privacy and authorization as executable code.** A policy page protects
   nobody. The deletion is a scheduled command, and the permission scope is a
   SQL predicate.
4. **Every external integration fails one day.** Price has a three source
   cascade with a circuit breaker. Balance comes from a pool of three servers.
   Nothing has a single upstream it cannot survive.
5. **What broke is written down.** With a date and a file reference, in the
   repository where it happened.

## What I do not do

- **No managed service by default.** Database, queue and storage run on owned
  hardware. When a third party service does enter, the reason is written in the
  repository.
- **No deploy that needs a human.** If shipping the new version requires
  somebody opening SSH, the work is not finished.
- **No private key on the server.** Anything touching Bitcoin runs watch only.
  Signing happens on the owner's device, off the machine that faces the internet.
- **No promising what does not run yet.** A project with no commits for months
  is labelled stable and quiet, not active. What is parked says it is parked.

## Reviewed by other people

Thirteen pull requests accepted across eight repositories owned by seven
different people, plus write access to somebody else's project.

- [**Blockstream/Jade**](https://github.com/Blockstream/Jade/pulls?q=is%3Apr+author%3ACaTeIM):
  five pull requests accepted into the official firmware of the Jade hardware
  wallet, starting with PR 260 in December 2025. Swapped buttons, USB JTAG,
  Windows connectivity, battery and power logic across T-Display, T-Display S3
  and Waveshare S3, and an i2c bus teardown fix. It is the firmware running on
  the Jade DIY boards. They show as closed rather than merged because the
  maintainers land the changes through their own branch.
- [**Origo**](https://github.com/oroderico/origo), by Oderico: another person's
  project, where I fix bugs with write access to the repository. It generates a
  BIP39 seed from human thrown dice, built after roughly 88 million dollars left
  Coldcard wallets through a build flag that lowered entropy unnoticed for five
  years.
- [**ai-memory**](https://github.com/akitaonrails/ai-memory/pulls?q=is%3Apr+author%3ACaTeIM),
  by Fábio Akita: three PRs accepted in June 2026. A native subcommand cut the
  Windows hook cost from around 735 ms to around 175 ms per tool call. The other
  two stopped deleting third party hooks and stopped polluting someone else's
  log. All with tests.
- [**FrankMD, Home Assistant and others**](https://github.com/search?q=is%3Apr+author%3ACaTeIM+is%3Amerged&type=pullrequests):
  three more accepted in FrankMD and fixes in two third party Home Assistant
  components, always with the test case that reproduces the problem.

---

<p align="center">
  <a href="https://selflabs.org">selflabs.org</a> ·
  <a href="https://store.selflabs.org">store.selflabs.org</a> ·
  contato@selflabs.org ·
  Vitória, Espírito Santo, Brazil
</p>

<p align="center"><sub>Leia em português em <a href="https://selflabs.org">selflabs.org</a>.</sub></p>
