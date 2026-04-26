# DuganLabs

A small constellation of products, all built on the same open-source substrate.

## Open source

- **[BaseNative](https://github.com/DuganLabs/basenative)** — signal-based web runtime + the meta-repo for our patterns. Auth, OG image rendering, virtual keyboard, admin tooling, shared lint/tsconfig, CLI scaffolding (`bn`). Everything we build for ourselves first lives here.
- **[T4BS](https://github.com/DuganLabs/t4bs)** — five-letter battle of bullshit. The flagship public showcase for what BaseNative enables. Live at [t4bs.com](https://t4bs.com).

## Proprietary

- **GreenPut** — building.
- **PendingBusiness** — building.
- **WarrenDugan** — personal site.

## Org-wide infrastructure

This repo (`DuganLabs/.github`) holds:

- **Reusable GitHub Actions workflows** at `.github/workflows/` — every project's `deploy.yml` is a thin caller. Cloudflare/Doppler credentials are passed in at call site; nothing project-specific embedded here.
- **Issue + PR templates** — consistent across the org.
- **Profile README** (this file) — the public face of DuganLabs.

## Pattern

> Build it open in BaseNative. Consume it everywhere. No proprietary business logic leaks into the open layer.

Every infra concern (lint, tsconfig, CI/CD, deploy, secrets) is defined once, in BaseNative or here, and consumed by every project — open and proprietary alike.
