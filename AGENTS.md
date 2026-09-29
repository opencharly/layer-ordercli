# AGENTS.md — layer-ordercli

Standalone candy repo for the `ordercli` layer — a Go CLI for food-delivery
order status (Foodora, Deliveroo, Glovo), installed with `go install`. The candy
lives in `charly.yml` at the repo root: the `require:` on `layer-golang`, the
`env:`/`path_append:` declarations, the `run:` install step, the `plan:`
checks, and the embedded `skill:` entity (the `ordercli-skill:` node) projected into the marketplace corpus
as `/charly-tools:ordercli`.

Canonical files:

- `charly.yml` — the `ordercli:` candy entity and the `ordercli-skill:` skill
  entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — user overview only; never agent guidance.

## Load these skills first (R0)

- `/charly-tools:ordercli` — the owning skill. The Foodora order-status CLI.
  Load before editing or troubleshooting.
- `/charly-image:layer` — the candy authoring reference (`charly.yml` schema,
  `plan:` step verbs incl. `check:` and `run:`, the `env:`/`path_append:`
  declarations, and service declarations). Load before editing any entity field
  or plan step.

## Build / validate / test

- The merge gate is the **org-wide** `charly/pr-validator` (required check
  `validate / validate`, defined in `opencharly/.github`); this repo has **no
  per-repo candy gate** and ships only `.github/workflows/tag-on-merge.yml`.
- The candy's `plan:` `check:` steps assert the binary lands at the fixed path
  and `ordercli --help` prints its provider subcommands. A live order query
  needs Foodora auth and is agent-graded.

## Modify this repo

- Edit the `ordercli:` candy entity AND the `ordercli-skill:` skill entity in
  `charly.yml` together. The skill is the projected usage source.
- Keep the `run:` install step and the `GOPATH`/`path_append:` declarations in
  step with the fixed binary path the checks assert.
- New behaviour claims belong in the `plan:` as an observable `check:` step, and
  in the skill body.

## Landing

- The authoritative rulebook is the umbrella `AGENTS.md` in
  `opencharly/opencharly` and `charly/AGENTS.md` in the charly repo — read it
  before landing.
- Release history lives in `CHANGELOG/`.
