## 1. Rename Private Content Repository

- [x] 1.1 Rename `private-content` → `private-hugo-theme` on GitHub (Settings → General → Repository name)
- [x] 1.2 Update local clone remote URL: `git remote set-url origin git@github.com:cearley/private-hugo-theme.git`
- [x] 1.3 Update `go.mod` module path in `private-hugo-theme` repo
- [x] 1.4 Push updated `go.mod` to `private-hugo-theme`

## 2. Move LICENSE to Theme Repository

- [x] 2.1 Copy `LICENSE` from public repo to `private-hugo-theme` repo root
- [x] 2.2 Commit and push LICENSE to `private-hugo-theme`
- [x] 2.3 Delete `LICENSE` from public repo (will be committed with other changes)

## 3. Update Public Repository

- [x] 3.1 Update `config.toml` module import path to `github.com/cearley/private-hugo-theme`
- [x] 3.2 Update `go.mod` to use new module path
- [x] 3.3 Run `go get github.com/cearley/private-hugo-theme@latest` to update dependency
- [x] 3.4 Verify local build works: `hugo build`
- [x] 3.5 Add note to README explaining theme is imported via Hugo Modules for license compliance

## 4. Update GitHub Actions Authentication

- [x] 4.1 Update `PRIVATE_REPO_PAT` scope to include `private-hugo-theme` (verified auto-followed rename)
- [x] 4.2 Verify PAT has read access to renamed repository

## 5. Create New Private Content Repository

- [x] 5.1 Create `private-content` repository on GitHub (private)
- [x] 5.2 Initialize with README describing content hub purpose
- [x] 5.3 Create directory structure per `docs/PRIVATE-CONTENT.md`:
  - `articles/`
  - `portfolio/`
  - `resume/`
  - `notes/`
- [x] 5.4 Initialize as Go module: `go mod init github.com/cearley/private-content`
- [x] 5.5 Add `hugo.toml` with appropriate mounts (for future content)

## 6. Verification

- [x] 6.1 Push public repo changes and verify GitHub Actions succeeds
- [x] 6.2 Verify deployed site renders correctly
- [x] 6.3 Confirm `private-hugo-theme` contains only theme + LICENSE
- [x] 6.4 Confirm `private-content` is ready for content hub architecture
