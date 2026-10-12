# Installation Guide

The Git repository remains the canonical source. A directory junction exposes its skills at the user-level without duplicating files.

The rest of this file assumes that you have cloned this repository locally and opened a terminal in the repository's root directory.

## 1. Add upstream remote

```bash
git remote add upstream https://github.com/mattpocock/skills
```

## 2. Create the user-level skills directory

User-level skills should be placed in `~/.copilot/skills/`. Create it if necessary:

Windows — PowerShell

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents\skills"
```

Linux / macOS — Bash

```bash
mkdir -p "$HOME/.agents/skills"
```

## 3. Links to the repository's skills

Create links pointing to all the directories containing skills.

Windows — PowerShell

```powershell
$repo = $PWD
$source = Join-Path $repo "skills"
$destination = "$HOME\.agents\skills"

New-Item -ItemType Directory -Force $destination | Out-Null

Get-ChildItem $source -Recurse -Filter "SKILL.md" -File |
    ForEach-Object {
        $skillDir = $_.Directory.FullName
        $skillName = $_.Directory.Name
        $link = Join-Path $destination $skillName

        if (Test-Path $link) {
            Write-Warning "Skill skipped since it already exists: $skillName"
        }
        else {
            New-Item -ItemType Junction `
                -Path $link `
                -Target $skillDir | Out-Null

            Write-Host "Skill linked: $skillName"
        }
    }
```

Linux / macOS — Bash

```bash
set -euo pipefail

repo=$pwd
source="$repo/skills"
destination="$HOME/.agents/skills"

mkdir -p "$destination"

while IFS= read -r -d '' skill_file; do
    skill_dir="$(dirname "$skill_file")"
    skill_name="$(basename "$skill_dir")"
    link="$destination/$skill_name"

    if [[ -e "$link" || -L "$link" ]]; then
        echo "Skill skipped since it already exists: $skill_name"
    else
        ln -s "$skill_dir" "$link"
        echo "Skill linked: $skill_name"
    fi
done < <(find "$source" -type f -name "SKILL.md" -print0)
```

The resulting structure is:

```text
~/.agents/skills/
├── ask-matt/  -- link to ->  <repository>/skills/engineering/ask-matt/
└── ...
```

## 4. Validate the installation

1. Open Copilot Chat in Agent mode.
2. Inspect available skills using the chat input's `/` menu or the *Open Customizations* menu.

## Uninstallation

It suffices to remove the links to all unwanted skills.
