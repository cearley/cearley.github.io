# Private Content Architecture

This document explains the architectural decisions behind using Hugo Modules to manage private content across multiple publishing targets.

## Overview

This site uses [Hugo Modules](https://gohugo.io/hugo-modules/) to import content from private repositories at build time. Private content never appears in the public repository—it's fetched during the Hugo build process and mounted into the content directory.

## Why Private Content?

### License Compliance

The Hugo Advance theme was purchased under the Zerostatic Pro License, which prohibits redistribution:

> You can't re-distribute or re-sell this theme as stock, in a tool or template.

Storing the theme in a public GitHub repository would violate this license. Hugo Modules allows the theme to remain in a private repository while still being used in the public site.

### Content Privacy

Some content (drafts, notes, resume data) should not be publicly visible but still needs to be version-controlled and available for builds.

## Content Hub Architecture

The private content repository serves as a **central content hub** that feeds multiple publishing targets:

```
┌─────────────────────────────────────┐
│         private-content             │
│         (Private Repo)              │
│                                     │
│  ├── portfolio/                     │
│  │   ├── projects/                  │
│  │   └── case-studies/              │
│  ├── articles/                      │
│  │   ├── ai-engineering/            │
│  │   ├── software-development/      │
│  │   └── career/                    │
│  ├── resume/                        │
│  │   ├── experience.yaml            │
│  │   ├── skills.yaml                │
│  │   └── education.yaml             │
│  └── notes/                         │
│      └── drafts/                    │
└─────────────────────────────────────┘
            │
            ▼
    ┌───────┴───────┬───────────────┬────────────────┐
    ▼               ▼               ▼                ▼
┌─────────┐   ┌──────────┐   ┌────────────┐   ┌───────────┐
│ Hugo    │   │ LaTeX    │   │ AI-Eng     │   │ LinkedIn  │
│ Website │   │ Resume   │   │ Website    │   │ (manual)  │
│         │   │          │   │            │   │           │
│ Modules │   │ Submod   │   │ Modules    │   │ Copy/     │
│         │   │          │   │            │   │ Export    │
└─────────┘   └──────────┘   └────────────┘   └───────────┘
```

### Design Principles

- **Organize by topic, not destination**: Content is grouped by subject matter (ai-engineering, career), not by where it will be published
- **Single source of truth**: One canonical version of each piece of content
- **Selective mounting**: Each target imports only the content paths it needs
- **Automatic propagation**: Updates to private-content propagate to all targets on rebuild

## Current Configuration

### This Site (cearley.github.io)

| Private Source | Mounted To |
|----------------|------------|
| `articles/software-development` | `content/en/posts` |
| `articles/ai-engineering` | `content/en/posts` |
| `articles/career` | `content/en/posts` |
| `portfolio/projects` | `content/en/portfolio/github` |
| `portfolio/case-studies` | `content/en/work` |

The theme is imported separately from `private-hugo-theme`.

### Other Targets

| Target | Integration Method | Rationale |
|--------|-------------------|-----------|
| **LaTeX Resume** | Git Submodules | LaTeX has no module system; needs full repo access |
| **AI-Engineering Site** | Hugo Modules | Same approach as this site |
| **LinkedIn** | Manual copy/export | Platform doesn't support automation |

## Hugo Modules vs Git Submodules

| Aspect | Hugo Modules | Git Submodules |
|--------|--------------|----------------|
| **Best for** | Hugo sites | Non-Hugo projects |
| **Mount flexibility** | Any path → any path | Fixed subdirectory only |
| **Version control** | go.mod/go.sum | Commit SHA pointer |

**Decision**: Use Hugo Modules for Hugo sites, git submodules for everything else.

## Related Documentation

- **README.md** - Development commands and workflows
- **CLAUDE.md** - Detailed development workflows and content structure
- **config.toml** - Module mount configuration (`[module]` section)
