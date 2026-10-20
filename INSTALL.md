# Installation Guide

The Git repository remains the canonical source. Symlinks (junctions on Windows) expose its skills at the user level without duplicating files.

The rest of this file assumes that you have cloned this repository locally and opened a terminal in the repository's root directory.

## 1. Add upstream remote

```bash
git remote add upstream https://github.com/mattpocock/skills
```

## 2. Create the user-level skills directory

User-level skills live in `~/.agents/skills/`. Create it if necessary:

Windows (PowerShell)

```powershell
New-Item -ItemType Directory -Force "$HOME\.agents\skills"
```

Linux / macOS (Bash or zsh)

```bash
mkdir -p "$HOME/.agents/skills"
```

## 3. Links to the repository's skills

Create a link for every skill. The `deprecated/` and `misc/` buckets are skipped on purpose.

Windows (PowerShell)

```powershell
$repo = $PWD
$source = Join-Path $repo "skills"
$destination = "$HOME\.agents\skills"

New-Item -ItemType Directory -Force $destination | Out-Null

Get-ChildItem $source -Recurse -Filter "SKILL.md" -File |
    Where-Object { $_.FullName.Substring($source.Length) -notmatch '^\\(deprecated|misc)\\' } |
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

Linux / macOS (Bash or zsh)

```bash
repo="$PWD"
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
done < <(find "$source" -type f -name "SKILL.md" -not -path "$source/deprecated/*" -not -path "$source/misc/*" -print0)
```

The resulting structure is:

```text
~/.agents/skills/
├── ask-matt/  -- link to ->  <repository>/skills/engineering/ask-matt/
└── ...
```

## 4. Validate the installation

1. Run `ls -l "$HOME/.agents/skills"`. Each skill should be a symlink (`->`) into this repo's `skills/` folder.
2. Open Copilot Chat in Agent mode.
3. Inspect available skills using the chat input's `/` menu or the *Open Customizations* menu.

## Uninstallation

It suffices to remove the links to all unwanted skills.
