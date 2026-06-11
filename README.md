# integrations-workflow

Hosts the reusable GitHub Actions workflow that publishes Meshery's integration content
to its downstream sites and registries.

## Usage

Called from `meshery/meshery` via `workflow_call`:

```yaml
jobs:
  integrations:
    uses: meshery-extensions/integrations-workflow/.github/workflows/publish.yml@master
    secrets: inherit
```

The driver in `meshery/meshery/.github/workflows/integrations-updater.yml` schedules and
dispatches this workflow; the implementation here checks out the needed source repos and
publishes the generated MDX/MD/JS into each downstream site.

## Required secrets

| Secret | Purpose |
|---|---|
| `MESHERY_CI` | PAT with push access to the publish targets |
| `INTEGRATION_SPREADSHEET_CRED` | Service-account JSON for the integrations spreadsheet |
| `MAIL_USERNAME` / `MAIL_PASSWORD` | SMTP credentials for failure notifications |

Pass them with `secrets: inherit` from the caller.

## Publish targets

The workflow checks out and pushes integration documentation to:

- [`meshery/meshery.io`](https://github.com/meshery/meshery.io) - Meshery's product site
- [`meshery/meshery`](https://github.com/meshery/meshery) - Meshery docs (in-tree)
- _all subscribed ecosystem partners_

## License

Apache 2.0. See [LICENSE](./LICENSE).
