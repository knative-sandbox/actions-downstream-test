# Downstream Test V1

This action allows you to target a downstream repository to upgrade with the
version of the upstream repository and then run the unit tests.

This action assumes go modules and repo setup is similar to Knative and that
environmental setup has already been performed.

## Usage

```yaml
- uses: knative-sandbox/downstream-test-go@v1
  with:
    # Upstream Repository. For example, knative/pkg
    # Default: ${{ github.repository }}
    upstream-repository: ""

    # The branch, tag or SHA to checkout for upstream-repository.
    # Defaults are the same as actions/checkout@v2.ref.
    upstream-ref: ""

    # Upstream Module. For example, knative.dev/pkg
    # Required.
    upstream-module: ""

    # Downstream Repository. For example, knative-sandbox/sample-controller
    # Required.
    downstream-repository: ""

    # The branch, tag or SHA to checkout for downstream-repository.
    # Defaults are the same as actions/checkout@v2.ref.
    downstream-ref: ""

    # Downstream Module. For example, knative.dev/sample-controller
    # Required.
    downstream-module: ""
```

## Scenarios

### Test knative.dev/pkg changes are accepted by knative.dev/sample-controller

```yaml
- uses: knative-sandbox/downstream-test-go@v1
  with:
    upstream-module: "knative.dev/pkg"
    downstream-repository: "knative-sandbox/sample-controller"
    downstream-module: "knative.dev/sample-controller"
```
