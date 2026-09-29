# ordercli

Food-delivery order status from the command line, as a charly layer — a Go CLI
covering Foodora, Deliveroo and Glovo.

The `ordercli` candy installs the `steipete/ordercli` Go binary into
`${HOME}/go/bin` with `go install`; it requires the `golang` toolchain. The
candy is verifiable because the installed binary lands at a fixed path, is an
executable file, and prints its delivery-provider subcommands when run with
`--help`. A live order-status query needs Foodora auth and is genuinely
free-form (agent-graded).

## What it provides

| Property | Value |
|---|---|
| Layer / candy | `ordercli` |
| Requires | `layer-golang` |
| Binary | `${HOME}/go/bin/ordercli` |
| Env | `GOPATH=~/go`; `PATH` append `~/go/bin` |
| Service / port | none |

## How to use it

Compose the layer in a box's `candy:` list:

```yaml
my-box:
  candy:
    base: fedora
    candy:
      - '@github.com/opencharly/layer-ordercli:v2026.243.0409'
```

Then run it inside the container:

```bash
charly shell my-box -c "ordercli --help"
```

## Layout

- `charly.yml` — the `ordercli:` candy entity (the `require:` dep, the `env:` /
  `path_append:`, the `run:` install step, and the `plan:` checks) plus the
  embedded `skill:` entity.
- `CHANGELOG/` — per-CalVer release history.
- `.github/workflows/tag-on-merge.yml` — CalVer tag + `CHANGELOG/` on merge.
- `README.md` — this user overview.

## Related

- Owning skill: `/charly-tools:ordercli` — the Foodora order-status CLI.
- Build dependency: `/charly-coder:golang`.
- Composed by: `/charly-openclaw:openclaw-full`.
- [`opencharly/opencharly](https://github.com/opencharly/opencharly) — the umbrella.
