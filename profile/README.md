# R&D GitHub Organization Standard

A small, practical GitHub structure for R&D teams. It is designed to be easy to explain to junior and mid-level developers while keeping project repositories isolated and consistent.

## Organization layout

```text
GitHub Organization
├── rnd-hub                 shared standards, onboarding, portfolio index
├── rnd-project-template    GitHub template repository for new projects
├── prj-001-<slug>          private project repository
├── prj-002-<slug>          private project repository
└── ...
```

## Developer workflow

```text
Issue -> branch -> implement -> test -> pull request -> review -> merge
```

## Repository roles

- `rnd-all`: Read access to `rnd-hub` and `rnd-project-template`.
- `rnd-prj-XXX`: Write access to its project repository.
- Project lead, when needed: Maintain access to that project repository.
- Organization owners: administrative access.

Keep organization base repository permission at **None** and grant access through teams.

## New project

1. Create a repository from `rnd-project-template`.
2. Name it `prj-XXX-<short-slug>`.
3. Run the bootstrap script locally:

```bash
python scripts/bootstrap_project.py \
  --id PRJ-003 \
  --name "Forecast Platform" \
  --slug forecast-platform \
  --owner github-username \
  --team rnd-prj-003 \
  --org your-org \
  --workstreams ml,backend
```

4. Edit `README.md` and `docs/technical-overview.md`.
5. Add the repository to `rnd-hub/portfolio/projects.yaml`.
6. Apply the GitHub repository settings in `rnd-hub/runbooks/create-project.md`.

## Design principles

- One repository per R&D product/project by default.
- Workstreams such as `ml/`, `backend/`, `ui/`, and `ops/` exist only when needed.
- `.rnd/project.toml` is the repository-local source of truth for project identity and enabled workstreams.
- Documentation templates live only in `rnd-hub/templates/` to avoid duplicated copies.
- Do not commit secrets, large datasets, model weights, checkpoints, or generated build artifacts.
