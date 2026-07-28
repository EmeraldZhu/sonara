# Lunara

> This is a fork of [Lunara](https://github.com/Blueturboguy07/lunara) by
> [Blueturboguy07](https://github.com/Blueturboguy07). Unlike the upstream
> repo, this fork publishes a bundled, compiled Android APK on the
> [Releases page](../../releases) — download it and install it directly, no
> build step required. All credit for the original app goes to the upstream
> project.

> **⚠️ Unfinished — this is a work in progress.**
> Lunara is not on the App Store or Google Play. Features are landing
> continuously and things will break. Do not rely on it as your only record of
> your health data.

**An open-source, local-first cycle, fertility, pregnancy, and perimenopause companion.**

Lunara ships through native iOS and Android shells powered by Capacitor. Core
tracking works without an account or Lunara-hosted user database. Optional
backup and AI features transmit data only after you enable them; their scope and
security boundaries are documented in the repository.

Lunara is an open-source alternative to Flo®. It is not affiliated with, endorsed by, or connected to Flo Health Inc.

## Why

- **No subscription gate.** Tracking, pattern insights, reports, pregnancy
  guidance, and perimenopause tools are part of the open-source app.
- **Local first by architecture.** Core logs live in the app's local storage.
  Optional backup stores a client-encrypted blob; optional AI shares only the
  categories you select for that request.
- **No 54-screen onboarding funnel. No paywall gauntlet. No nagging.**

---

## Getting Lunara onto your phone

Download the latest APK from the [Releases page](../../releases) and install
it on your Android phone. No build step, no cable, no developer setup.

## Structure

- `app/` — React/Vite product layer plus Capacitor iOS and Android projects
- `workers/backup/` — stateless zero-knowledge backup relay (Cloudflare Worker + R2)
- `workers/reminders/` — opt-in generic email reminders (no health terms, ever)
- `docs/NATIVE_ARCHITECTURE.md` — current runtime and platform design
- `docs/FEATURE_PARITY.md` — honest implementation and release-readiness map

## Develop

```sh
pnpm install
pnpm dev      # run the app in a browser
pnpm test     # engine unit tests
pnpm --filter @lunara/app native:sync
```

The cycle engine is covered by a seeded fuzz audit
(`app/src/engine/estimateAudit.test.ts`) that exercises every user-facing
estimate across 360 generated histories. It must stay at zero violations —
run `pnpm test` before touching any prediction math.

## The AI companion is optional and bring-your-own-key

Lunara ships no shared API key and works fully without AI. If you enable it, you
supply your own credential:

- **Anthropic** — an API key, or a token from `claude setup-token` to bill
  answers to a Claude subscription instead of API credits.
- **OpenAI** — a project API key.

Credentials are stored in the iOS Keychain / Android Keystore, never in the
cycle database and never in a backup. Nothing from your tracker is sent unless
you tick the specific categories for that message.

## Disclaimer

Lunara is not a medical device and does not diagnose, treat, cure, or prevent any condition. Predictions are estimates for informational purposes only and must not be used to prevent pregnancy.

## License

AGPL-3.0 — see [LICENSE](LICENSE).
