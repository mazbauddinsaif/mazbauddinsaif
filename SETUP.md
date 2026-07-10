# Setup — Profile README (mazbauddinsaif)

Dynamic GitHub profile README, adapted from [Andrew6rant/Andrew6rant](https://github.com/Andrew6rant/Andrew6rant).
Left side shows an ASCII-art portrait generated from your photo; right side shows live GitHub stats (repos, stars, commits, followers, lines of code, uptime since birthday), auto-updated daily by GitHub Actions.

## 1. Before pushing — do these locally

1. **Review the personal info** in `dark_mode.svg` / `light_mode.svg` (OS, IDE, languages, hobbies, emails, LinkedIn, Discord). Edit the text values directly — they are plain `<tspan>` elements. Keep the `id="..."` tspans intact (the script updates those). Birthday is already set in `today.py` (`BIRTHDAY`).

2. *(Optional)* Preview locally by opening `dark_mode.svg` in a browser.

## 2. Push

The repo already exists (`mazbauddinsaif/mazbauddinsaif`) and this folder is already connected to it with the commit prepared. Just:

```
git push origin main
```

## 3. Configure secrets (required for the Action)

Repo → Settings → Secrets and variables → Actions → New repository secret:

- `USER_NAME` = `mazbauddinsaif`
- `ACCESS_TOKEN` = a **fine-grained personal access token** (github.com → Settings → Developer settings → Fine-grained tokens) with **All repositories** access and:
  - Account permissions: read:Followers, read:Starring, read:Watching
  - Repository permissions: read:Commit statuses, read:Contents, read:Issues, read:Metadata, read:Pull Requests

## 4. Done

The workflow (`.github/workflows/build.yaml`) runs on every push to `main` and daily at 04:00 UTC. It fills in the stats and commits the updated SVGs. First run may take a while (it counts lines of code across all your repos; later runs use `cache/`).

To test locally instead of waiting for the Action:

```
pip install -r cache/requirements.txt
set ACCESS_TOKEN=ghp_yourtoken
set USER_NAME=mazbauddinsaif
python today.py
```
