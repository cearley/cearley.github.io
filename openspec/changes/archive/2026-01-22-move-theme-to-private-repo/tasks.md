# Tasks: Move Hugo Advance Theme to Private Repository

## 1. Create Private Content Repository

- [x] 1.1 Create `private-content` repository on GitHub (private)
- [x] 1.2 Initialize repository with README
- [x] 1.3 Create `themes/hugo-advance/` directory structure

## 2. Migrate Theme Files

- [x] 2.1 Copy `themes/hugo-advance/` contents to private repo
- [x] 2.2 Commit and push theme to private repo
- [x] 2.3 Verify theme files are complete in private repo (1858 files)

## 3. Configure Hugo Modules (Public Repo)

- [x] 3.1 Run `hugo mod init github.com/cearley/cearley.github.io`
- [x] 3.2 Add `[module]` configuration to `config.toml`
- [x] 3.3 Test locally with `hugo mod get -u && hugo server`
- [x] 3.4 Verify site renders correctly with module-imported theme (8 pages, 1636 static files)

## 4. Configure GitHub Actions Authentication

- [x] 4.1 Create fine-grained PAT with read access to `private-content`
- [x] 4.2 Add `PRIVATE_REPO_PAT` secret to public repository
- [x] 4.3 Update `.github/workflows/hugo.yaml`:
  - [x] 4.3.1 Add Go setup step
  - [x] 4.3.2 Add git config for PAT authentication
  - [x] 4.3.3 Add `GOPRIVATE` environment variable

## 5. Remove Theme from Public Repository

- [x] 5.1 Delete `themes/hugo-advance/` directory from public repo
- [x] 5.2 Update `.gitignore` (added build artifacts)
- [x] 5.3 Commit removal (separate commit for clear history)

## 6. Verification

- [x] 6.1 Run `hugo mod graph` to verify module dependency
- [x] 6.2 Test full build locally (19 pages, 1811 static files)
- [x] 6.3 Push to branch and verify GitHub Actions workflow succeeds
- [x] 6.4 Verify deployed site renders correctly
- [x] 6.5 Confirm public repo no longer contains theme files (404 on themes/)
