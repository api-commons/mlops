# MLOps and Model Registry

The common machine-learning-operations vocabulary -- models in a registry, their versions, datasets, experiments and the runs and training jobs inside them -- distilled from the APIs that already exist. Part of [Schema Commons](https://github.com/api-commons/schema-commons),
published by the [API Commons](https://apicommons.org).

Built from the providers tagged MLOps, Machine Learning, Model Registry, Experiment Tracking, Data Science, Model Training, AI Infrastructure in [APIs.io](https://apis.io) that
publish their own OpenAPI. Only harvested contracts count -- nothing API Evangelist
generated. Every number below is a count of providers.

## What the market already agrees on

<!-- commons:summary -->
| Concept | Expose it | Readable schema | Core properties (share) | Collection named |
| --- | ---: | ---: | --- | --- |
| ml_model | 99 | 87 | id 66%, name 55% | models 94, model 7, registered_models 1 |
| dataset | 36 | 35 | name 83%, id 69%, created_at 60% | datasets 32, dataset 9 |
| experiment | 14 | 14 | created_at 86%, id 86%, name 86%, status 79% | experiments 13, experiment 2 |
| training_run | 33 | 30 | id 80%, status 70%, created_at 57% | runs 28, jobs 2, trainings 2, fine_tuning 1 |

Cohort: 342 providers with harvested OpenAPI, 126 crosswalks. Of the providers exposing a ml_model: 28% create, 92% list, 48% fetch, 18% update, 28% delete. Generated 2026-11-11 by build.py.
<!-- /commons:summary -->

Shares are of the providers with a readable resource schema for that concept. The
extended tier and the long tail of every concept are in [profile.yml](profile.yml).

## What the measurement shows

- Experiments are the best-agreed MLOps resource: id, name, created_at and status, with description, metadata and tags at 36%.
- Datasets agree on name, id and created_at. Training runs agree on id, status and created_at -- a run is a job whose metrics and parameters are shaped by each platform.
- Models are exposed by 99 providers and agree only on id and name, because a model list is also the inference-catalogue GET /models that api-commons/models standardizes. The registry and the inference catalogue share a path, not a resource.

## Artifacts

- [openapi.yml](openapi.yml) -- OpenAPI 3.1 of the shared operations. No one serves it; it
  is the shape to map to. Lints clean against the
  [naming ruleset](https://github.com/api-commons/schema-commons/blob/main/ruleset/schema-commons-naming.yaml).
- [schema/](schema) -- JSON Schema 2020-12 per concept; each property carries
  `x-commons-tier`, `x-commons-share`, `x-commons-providers` and the spellings seen.
- [crosswalk/](crosswalk) -- one per provider, common name -> their name, with the harvested
  spec and operations each mapping was read from.
- [adopters.yml](adopters.yml) -- who exposes which concept, linked to their APIs.io page.
- [concepts.yml](concepts.yml) -- the only hand-written input: concepts, path segments and
  their qualifiers, aliases, reviewed exclusions, merged duplicates, and the decisions below.
- [census/](census) -- the cohort and the raw census the profile is built from.

## Decisions

These are calls, not measurements, recorded so they can be revisited as the method matures.

- ml_model and training_run carry role names: model is the inference catalogue in models, and run and job are used across ci-cd and workflow-automation.

## Rebuild

```bash
../schema-commons/scripts/run.sh .
```

## License

Artifacts CC BY-NC-SA 4.0 ([LICENSE](LICENSE)); code Apache 2.0 ([LICENSE-CODE](LICENSE-CODE)).
