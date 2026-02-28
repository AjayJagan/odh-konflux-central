# Models-as-a-Service Integration Test

This directory contains the Konflux integration test pipeline for Models-as-a-Service (MaaS).

## Repositories

- **Pipeline config:** [opendatahub-io/odh-konflux-central](https://github.com/opendatahub-io/odh-konflux-central)
- **Tested project:** [opendatahub-io/models-as-a-service](https://github.com/opendatahub-io/models-as-a-service)

## What This Pipeline Does

The `pr-test-pipelinerun.yaml` defines a Tekton pipeline that:

1. **Parses metadata** from the Konflux Snapshot (event type, component info, git URLs, etc.)
2. **Checks prerequisites** — skips cluster provisioning for push events (runs only for PR events)
3. **Provisions an ephemeral Hypershift cluster** on AWS via EaaS (Ephemeral-as-a-Service)
4. **Runs e2e tests** — clones the component source, deploys Open Data Hub operator from the Snapshot, and executes the MaaS smoke tests against the ephemeral cluster

## Metadata

Test metadata (event type, pull request number, source/target git URLs, component info, etc.) is defined by the shared Konflux integration test task:

**[test_metadata.yaml](https://github.com/konflux-ci/integration-examples/blob/main/tasks/test_metadata.yaml)**
