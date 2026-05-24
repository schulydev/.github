<p align="center">
  <img src="https://raw.githubusercontent.com/schulydev/Schuly/main/assets/app_icon.png" width="160" alt="Schuly Logo">
</p>

<h1 align="center">Schuly</h1>

<p align="center">
  <strong>The better Schulnetz app — open-source, mobile-first, extensible.</strong>
</p>

<p align="center">
  <a href="https://schuly.dev"><img src="https://img.shields.io/badge/site-schuly.dev-3da8ff" alt="Website"/></a>
  <a href="https://github.com/schulydev/Schuly/releases"><img src="https://img.shields.io/github/v/release/schulydev/Schuly?include_prereleases&color=3da8ff&label=App%20Release" alt="App Release"/></a>
  <a href="https://github.com/schulydev/Schuly/stargazers"><img src="https://img.shields.io/github/stars/schulydev/Schuly?style=flat&color=3da8ff" alt="Stars"/></a>
</p>

---

## What is Schuly?

A modern, mobile-first alternative to the official Schulnetz client — built around a clean Flutter UI, a clean-architecture C# backend, and a plugin runtime that lets new school systems plug in without touching the core.

> Schuly is **NOT** affiliated with, endorsed by, or connected to Schulnetz or Centerboard AG.

## Repositories

| Repo | Stack | Purpose |
|---|---|---|
| [**Schuly**](https://github.com/schulydev/Schuly) | Flutter / Dart | The mobile app — iOS + Android |
| [**SchulyBackend**](https://github.com/schulydev/SchulyBackend) | C# / ASP.NET Core | API + domain logic + plugin host |
| [**SchulyPluginAbstractions**](https://github.com/schulydev/SchulyPluginAbstractions) | C# / NuGet | Stable plugin contract — implement this to write a plugin |
| [**SchulyPlugins**](https://github.com/schulydev/SchulyPlugins) | C# | Official plugins (Schulware, Example, ...) |
| [**SchulyWebsite**](https://github.com/schulydev/SchulyWebsite) | Angular | Landing site at [schuly.dev](https://schuly.dev) |

## Architecture at a glance

```
        ┌────────────┐
        │  Schuly    │  Flutter mobile app
        │  (mobile)  │
        └─────┬──────┘
              │ REST / OpenAPI
              ▼
   ┌────────────────────┐       ┌────────────────────────────┐
   │   SchulyBackend    │◄──────│  SchulyPluginAbstractions  │
   │   ASP.NET Core     │       │  (NuGet contract)          │
   │   PostgreSQL + EF  │       └─────────────▲──────────────┘
   │   Plugin host      │                     │ implements
   └─────────▲──────────┘                     │
             │                       ┌────────┴────────┐
             │ discovers + runs ────►│  SchulyPlugins  │
             │                       │  (Schulware, …) │
             │                       └─────────────────┘
             ▼
       OIDC provider
```

## Want to contribute?

- 🐛 Bugs → open an issue in the affected repo with the `bug` label
- ✨ Features → open an issue with `feature` or `enhancement`
- 🧩 New plugin → see [SchulyPlugins](https://github.com/schulydev/SchulyPlugins) and the [PluginAbstractions](https://github.com/schulydev/SchulyPluginAbstractions) contract

Every repo follows the same workflow: open an issue with a label, branch as `feature/<#>_PascalCase` or `fix/<#>_PascalCase`, open a PR, squash-merge.
