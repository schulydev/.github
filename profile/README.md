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

```mermaid
---
config:
  layout: elk
  look: neo
  theme: base
  themeVariables:
    edgeLabelBackground: '#ffffff'
    tertiaryColor: '#ffffff'
    tertiaryTextColor: '#000000'
    tertiaryBorderColor: '#ffffff'
  flowchart:
    nodeSpacing: 50
    rankSpacing: 70
---
flowchart TB
  %% === Clients ===
  Schuly["Schuly · Flutter"]:::client
  WebUI["Web UI · Angular"]:::clientPlanned

  %% === Backend ===
  Backend["SchulyBackend<br/><i>ASP.NET Core</i>"]:::backend
  DB@{ shape: cyl, label: "PostgreSQL" }

  %% === Plugin system ===
  Abstractions["SchulyPluginAbstractions<br/><i>NuGet</i>"]:::contract

  subgraph plugins["SchulyPlugins"]
    direction TB
    Example["Plugin.Example"]:::plugin
    Schulware["Plugin.Schulware"]:::plugin
  end
  class plugins region

  %% === External ===
  OIDC["OIDC Provider"]:::ext
  SchulwareAPI["SchulwareAPI"]:::ext
  Schulnetz["Schulnetz"]:::ext

  %% === Edges ===
  Schuly -->|REST| Backend
  WebUI -->|REST| Backend
  Schuly <-->|auth| OIDC
  WebUI <-->|auth| OIDC
  Backend <-->|validate| OIDC
  Backend --- DB
  Backend -. depends on .-> Abstractions
  Backend ==>|runs| plugins
  Example -. implements .-> Abstractions
  Schulware -. implements .-> Abstractions
  Schulware --> SchulwareAPI
  SchulwareAPI --> Schulnetz
  class DB db

  %% === Arrows ===
  linkStyle default stroke:#9ca3af,stroke-width:1.5px,color:#000000

  %% === Node Styles ===
  classDef client        fill:#3da8ff,stroke:#1c6ec0,color:#fff
  classDef clientPlanned fill:#3da8ff,stroke:#1c6ec0,color:#fff,stroke-dasharray: 5 4
  classDef backend       fill:#512bd4,stroke:#341a8a,color:#fff
  classDef db            fill:#336791,stroke:#1e3f5c,color:#fff
  classDef contract      fill:#a36ee0,stroke:#6e44b8,color:#fff
  classDef plugin        fill:#ffc658,stroke:#c89a3e,color:#000
  classDef ext           fill:#6c757d,stroke:#3d4449,color:#fff
  classDef region        fill:transparent,stroke:#888,color:#888,stroke-dasharray: 4 4
```

## Want to contribute?

- 🐛 Bugs → open an issue in the affected repo with the `bug` label
- ✨ Features → open an issue with `feature` or `enhancement`
- 🧩 New plugin → see [SchulyPlugins](https://github.com/schulydev/SchulyPlugins) and the [PluginAbstractions](https://github.com/schulydev/SchulyPluginAbstractions) contract

Every repo follows the same workflow: open an issue with a label, branch as `feature/<#>_PascalCase` or `fix/<#>_PascalCase`, open a PR, squash-merge.
