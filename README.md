# keepassxc

KeePassXC password manager layer for OpenCharly images.

The `keepassxc` candy installs the `keepassxc` package, which ships the
KeePassXC GUI at `/usr/bin/keepassxc` (launched on-demand inside a desktop
session) and the `keepassxc-cli` console tool at `/usr/bin/keepassxc-cli`. The
CLI runs headless, so its presence and `--version` output are deterministically
verifiable in a disposable container; the GUI's interactive use is graded
against a live desktop deployment that composes this candy.

This candy is the **GUI** for editing `.kdbx` databases. It is distinct from
`charly secrets` (`/charly-build:secrets`), which talks to the Secret Service
system keyring — it reads a KeePassXC database only via the app's FdoSecrets /
Secret Service exposure.

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `keepassxc` |
| Package | `keepassxc` (rpm + pac) |
| Binaries | `/usr/bin/keepassxc` (GUI), `/usr/bin/keepassxc-cli` |
| Install files | `charly.yml` (package only) |
| Service / port | none (on-demand GUI) |

## How to use it

Compose the layer by pinning this repo in a box's `candy:` list, typically on a
desktop base:

```yaml
my-desktop:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-keepassxc:v2026.239.1624'
```

After the image is built:

```bash
keepassxc-cli --version
keepassxc --version
```

## Layout

- `charly.yml` — the `keepassxc:` candy entity: the `package:` section, the
  `check:` assertions, and the embedded `skill:` entity.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-infrastructure:keepassxc` — the KeePassXC password manager candy
- Host Secret Service provider: `/charly-infrastructure:keepassxc-keyring`
- charly credential store: `/charly-build:secrets` (Secret Service + GPG)
- [`opencharly/charly`](https://github.com/opencharly/charly) — the charly CLI and image builder
- [`opencharly/opencharly`](https://github.com/opencharly/opencharly) — the umbrella
