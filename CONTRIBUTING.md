# Contributing to Reliquia

Reliquia is built in two repositories. This page covers the shared parts: where each
document lives, getting both repositories working locally, and how a change reaches
`main`. Each repository's docs site is the source of truth; this page links to it and
does not restate it.

## Two repositories

| Repository                                             | Owns                                                                                                         | Never contains        | Docs                                       |
| ------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ | --------------------- | ------------------------------------------ |
| [`reliquia`](https://github.com/playreliquia/reliquia) | The Godot 4 client, dedicated server and bot; the Nakama Go plugin; the web site; the CI that publishes them | Cluster configuration | <https://playreliquia.github.io/reliquia/> |
| [`platform`](https://github.com/playreliquia/platform) | The cluster and its environment: k3s, Flux, Agones, Nakama's deployment, Postgres, secrets, DNS              | Game code             | <https://playreliquia.github.io/platform/> |

The game repo publishes images; the platform repo pins them by tag and Renovate opens the
bump when a new tag appears. Why they are separate:
[platform ADR-0012](https://playreliquia.github.io/platform/internal/adr/0012-separate-game-and-platform-repos/).

## Documentation map

New to the project: read the reliquia [Introduction][r-intro], then the
[reliquia][r-arch] and [platform](https://playreliquia.github.io/platform/architecture/)
architecture pages, then the glossary of the repository you will work in.

### reliquia

| Page                                                                                   | When                                                             |
| -------------------------------------------------------------------------------------- | ---------------------------------------------------------------- |
| [Introduction][r-intro]                                                                | First; what the repository is and where things live              |
| [Architecture][r-arch]                                                                 | Before touching more than one artifact                           |
| [Operations: CI][r-ci]                                                                 | When a pull request check fails                                  |
| [Runbooks][r-runbooks]                                                                 | The index of every manual step                                   |
| [Local development][r-localdev]                                                        | First checkout; every day                                        |
| [Godot toolchain](https://playreliquia.github.io/reliquia/runbooks/godot-toolchain/)   | When the Godot download fails, or the export templates are stale |
| [Release](https://playreliquia.github.io/reliquia/runbooks/release/)                   | Cutting a version, a hotfix, a rollback                          |
| [Organisation setup][r-orgsetup]                                                       | Organisation owners only; also holds the cross-repo contracts    |
| [Rename checklist](https://playreliquia.github.io/reliquia/runbooks/rename-checklist/) | When the organisation or game name changes                       |
| [Glossary][r-glossary]                                                                 | When a term is unclear, or you are adding one                    |
| [Decisions](https://playreliquia.github.io/reliquia/internal/decisions/)               | Before reopening a settled question                              |

| ADR                                                                                           | Decides                                            |
| --------------------------------------------------------------------------------------------- | -------------------------------------------------- |
| [0001](https://playreliquia.github.io/reliquia/internal/adr/0001-release-model/)              | One lockstep version; the web image is exempt      |
| [0002](https://playreliquia.github.io/reliquia/internal/adr/0002-nakama-plugin-build/)        | How the Nakama plugin builds against Nakama's deps |
| [0003](https://playreliquia.github.io/reliquia/internal/adr/0003-zone-credential-and-limits/) | The zone credential and its limits                 |
| [0004](https://playreliquia.github.io/reliquia/internal/adr/0004-testing-strategy/)           | Testing strategy                                   |
| [0005](https://playreliquia.github.io/reliquia/internal/adr/0005-nakama-godot-vendored/)      | nakama-godot vendored at a pinned commit           |
| [0006](https://playreliquia.github.io/reliquia/internal/adr/0006-godot-via-mise/)             | The Godot editor installed by a mise task          |

### platform

| Page                                                                                                     | When                                                         |
| -------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------ |
| [Architecture](https://playreliquia.github.io/platform/architecture/)                                    | Before any change; the three layers and who owns each        |
| [Operations][p-ops]                                                                                      | Standing up an environment; the runbooks in first-time order |
| [Operations: CI](https://playreliquia.github.io/platform/operations/ci/)                                 | When a pull request check fails                              |
| [Rolling back a game release](https://playreliquia.github.io/platform/operations/rollback/)              | When a deployed image has to go back                         |
| [Runbooks](https://playreliquia.github.io/platform/runbooks/)                                            | The index of every manual step                               |
| [VPS and k3s](https://playreliquia.github.io/platform/runbooks/vps-k3s/)                                 | Provisioning or converging a host                            |
| [Flux bootstrap](https://playreliquia.github.io/platform/runbooks/flux-bootstrap/)                       | Pointing a new cluster at this repository                    |
| [SOPS and age keys][p-sops]                                                                              | Getting secrets access; onboarding or offboarding someone    |
| [Postgres backup and restore](https://playreliquia.github.io/platform/runbooks/postgres-backup-restore/) | Checking backups; running a restore                          |
| [Alerts](https://playreliquia.github.io/platform/runbooks/alerts/)                                       | When an alert fires in Discord                               |
| [OpenTofu bootstrap](https://playreliquia.github.io/platform/runbooks/opentofu-bootstrap/)               | Changing DNS, R2 buckets or edge tokens                      |
| [EU bring-up](https://playreliquia.github.io/platform/runbooks/eu-bring-up/)                             | When the second region's VPS is ordered                      |
| [Status page](https://playreliquia.github.io/platform/runbooks/status-page/)                             | Changing what status.playreliquia.com checks                 |
| [Scaleway Transactional Email](https://playreliquia.github.io/platform/runbooks/scaleway-tem/)           | Account mail: sending domain and credentials                 |
| [The automation App](https://playreliquia.github.io/platform/runbooks/automation-app/)                   | When Renovate or release-please stop acting                  |
| [After the import](https://playreliquia.github.io/platform/runbooks/post-import/)                        | Record of the one-time move to `playreliquia/platform`       |
| [Rename checklist](https://playreliquia.github.io/platform/runbooks/rename-checklist/)                   | When the organisation or game name changes                   |
| [Glossary](https://playreliquia.github.io/platform/internal/glossary/)                                   | When a term is unclear, or you are adding one                |
| [Decisions](https://playreliquia.github.io/platform/internal/decisions/)                                 | Before reopening a settled question                          |

| ADR                                                                                                          | Decides                                                        |
| ------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------- |
| [0001](https://playreliquia.github.io/platform/internal/adr/0001-zensical-over-mkdocs-material/)             | Zensical over MkDocs Material                                  |
| [0002](https://playreliquia.github.io/platform/internal/adr/0002-mise-as-task-runner/)                       | mise as the task runner                                        |
| [0003](https://playreliquia.github.io/platform/internal/adr/0003-local-pre-commit-hooks/)                    | Local pre-commit hooks via mise                                |
| [0004](https://playreliquia.github.io/platform/internal/adr/0004-kyverno-for-admission-control/)             | Kyverno for admission control, audit first                     |
| [0005](https://playreliquia.github.io/platform/internal/adr/0005-gitleaks-trivy-ci-scanning/)                | gitleaks and Trivy in CI                                       |
| [0006](https://playreliquia.github.io/platform/internal/adr/0006-validation-and-testing-strategy/)           | Validation and testing strategy                                |
| [0007](https://playreliquia.github.io/platform/internal/adr/0007-toolchain-pinning-boundary/)                | Toolchain pinning and the cluster-state boundary               |
| [0008](https://playreliquia.github.io/platform/internal/adr/0008-single-node-k3s-on-ovh-vps/)                | Single-node k3s on an OVH VPS                                  |
| [0009](https://playreliquia.github.io/platform/internal/adr/0009-sops-age-over-external-secrets/)            | SOPS and age over External Secrets                             |
| [0010](https://playreliquia.github.io/platform/internal/adr/0010-cloudflare-r2-and-opentofu/)                | Cloudflare R2 and OpenTofu for the edge                        |
| [0011](https://playreliquia.github.io/platform/internal/adr/0011-agones-for-game-servers/)                   | Agones for game servers                                        |
| [0012](https://playreliquia.github.io/platform/internal/adr/0012-separate-game-and-platform-repos/)          | Separate game and platform repositories                        |
| [0013](https://playreliquia.github.io/platform/internal/adr/0013-traefik-gateway-api-cert-manager/)          | Traefik, Gateway API and cert-manager DNS-01                   |
| [0014](https://playreliquia.github.io/platform/internal/adr/0014-k3d-e2e-and-flate-validation/)              | k3d end-to-end tests and flate validation                      |
| [0015](https://playreliquia.github.io/platform/internal/adr/0015-k3s-ansible-and-system-upgrade-controller/) | k3s-ansible to bootstrap, system-upgrade-controller to upgrade |
| [0016](https://playreliquia.github.io/platform/internal/adr/0016-kured-game-aware-reboots/)                  | kured with game-aware reboot blocking                          |
| [0017](https://playreliquia.github.io/platform/internal/adr/0017-per-environment-sops-keys/)                 | Per-environment SOPS keys                                      |
| [0018](https://playreliquia.github.io/platform/internal/adr/0018-post-deploy-smoke-tests/)                   | Post-deploy smoke tests                                        |
| [0019](https://playreliquia.github.io/platform/internal/adr/0019-ssh-open-rate-limited-keys-only/)           | SSH open, rate limited, keys only                              |
| [0020](https://playreliquia.github.io/platform/internal/adr/0020-public-status-page/)                        | The public status page on Gatus                                |
| [0021](https://playreliquia.github.io/platform/internal/adr/0021-alertmanager-routing-to-discord/)           | Alertmanager routes curated alerts to Discord                  |

## Local setup

Both repositories are private: you need membership of the `playreliquia` organisation
before you can clone them.

### Prerequisites

| Tool                                                       | Why                                                                                                                                                                                                                                                                                                                                               |
| ---------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| git, with an SSH key on your GitHub account                | Cloning and pushing                                                                                                                                                                                                                                                                                                                               |
| [mise](https://mise.jdx.dev/installing-mise.html)          | The only tool you install by hand. It installs every other tool at the version in `.mise/config.toml`, checked against `.mise/mise.lock` ([platform ADR-0002](https://playreliquia.github.io/platform/internal/adr/0002-mise-as-task-runner/), [ADR-0007](https://playreliquia.github.io/platform/internal/adr/0007-toolchain-pinning-boundary/)) |
| Docker with Compose                                        | reliquia's local stack (`mise run dev`), integration tests and image builds                                                                                                                                                                                                                                                                       |
| An `ssh-ed25519` key at `~/.ssh/id_ed25519`, or an age key | platform only: decrypting secrets. [SOPS and age keys][p-sops] lists the key types that work                                                                                                                                                                                                                                                      |

Activate mise in your shell once, as its install page describes, so each repository's
tools are on `PATH` when you `cd` into it.

### Clone both repositories side by side

```sh
mkdir reliquia && cd reliquia
git clone git@github.com:playreliquia/reliquia.git
git clone git@github.com:playreliquia/platform.git
```

### Set up reliquia

```sh
cd reliquia
mise install            # every pinned tool; its postinstall hook runs `mise run setup`
mise run godot:install  # the Godot editor and export templates
mise run dev            # build and start the Compose stack, launch two clients
mise run dev:down       # stop and remove the stack
```

`mise run setup` runs `uv sync`, installs the pre-commit hooks and sets `pull.rebase`
and `fetch.prune` for the repository. The Godot editor is not a mise tool; the
[Godot toolchain][r-godot] runbook and [ADR-0006](https://playreliquia.github.io/reliquia/internal/adr/0006-godot-via-mise/)
say why. The per-component loop (editor, one rebuilt service, content validation, the
web image) and allocation simulation are in [Local development][r-localdev].

### Set up platform

```sh
cd platform
mise install              # every pinned tool; its postinstall hook runs `mise run setup`
mise run render           # render the Flux trees into .render/
mise run render:check     # fail on an unresolved or empty substitution
mise run test:flux        # every Kustomization and HelmRelease renders and resolves
mise run validate         # manifests against Kubernetes and CRD schemas
mise run test:policies    # Kyverno policy tests, no cluster needed
mise run test:alerts      # PrometheusRules and the Alertmanager config
```

None of these need a cluster or a secret. The end-to-end bring-up on k3d runs in CI
([Operations: CI](https://playreliquia.github.io/platform/operations/ci/)).

Reading or editing an encrypted `*.sops.yaml` file needs your key added as a recipient:
send your public key to a maintainer and follow "Onboard a maintainer" in
[SOPS and age keys][p-sops]. Confirm with `sops decrypt` on one file. Cluster and host
access follow the [Operations][p-ops] order and are granted by a maintainer.

### Check it worked

In each repository:

```sh
mise tasks      # every task with its description
mise run lint   # what CI runs on every pull request; must pass before you start
mise run docs   # serve that repository's docs site locally
```

## Making a change

1. Branch from `main`.
1. Run `mise run lint` plus the `check:*` and `test:*` tasks your change touches. A green
   local run is a green pull request: [reliquia CI][r-ci],
   [platform CI](https://playreliquia.github.io/platform/operations/ci/).
1. Title the pull request as a [Conventional Commit](https://www.conventionalcommits.org/)
   (`feat(scope): description`) and fill in the repository's pull request template.
1. `ci` is the one required check. `@playreliquia/maintainers` owns every path through
   `CODEOWNERS` and reviews.
1. A new or changed term goes in that repository's glossary in the same pull request. A
   decision someone could reasonably contest gets an ADR under `docs/internal/adr/`.

## Changes that cross both repositories

A game release is an image tag: reliquia publishes it, Renovate opens the pin bump in
platform, and merging that bump deploys it. Values both repositories must agree on
(image names, Agones annotations, Nakama environment variables, the Nakama endpoint)
are in the contracts table of [Organisation setup][r-orgsetup]. Change the producer
first, then the consumer, and link the two pull requests.

## Conduct and security

Everyone taking part follows the [Code of Conduct](CODE_OF_CONDUCT.md). Report
vulnerabilities as [SECURITY.md](SECURITY.md) describes, never in a public issue.

[r-intro]: https://playreliquia.github.io/reliquia/introduction/
[r-arch]: https://playreliquia.github.io/reliquia/architecture/
[r-ci]: https://playreliquia.github.io/reliquia/operations/ci/
[r-runbooks]: https://playreliquia.github.io/reliquia/runbooks/
[r-localdev]: https://playreliquia.github.io/reliquia/runbooks/local-dev/
[r-godot]: https://playreliquia.github.io/reliquia/runbooks/godot-toolchain/
[r-orgsetup]: https://playreliquia.github.io/reliquia/runbooks/org-setup/
[r-glossary]: https://playreliquia.github.io/reliquia/internal/glossary/
[p-ops]: https://playreliquia.github.io/platform/operations/
[p-sops]: https://playreliquia.github.io/platform/runbooks/sops/
