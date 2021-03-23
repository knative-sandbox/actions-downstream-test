# Downstream Test V1

This action allows you to target a downstream repository to upgrade with the
version of the upstream repository and then run the unit tests.

This action assumes go modules and repo setup is similar to Knative and that
environmental setup has already been performed.

## Usage

```yaml
- uses: knative-sandbox/actions-downstream-test@v1
  with:
    # Upstream Module. For example, knative.dev/pkg
    # Required.
    upstream-module: ""

    # Downstream Module. For example, knative.dev/sample-controller
    # Required.
    downstream-module: ""
```

## Scenarios

### Test knative.dev/pkg changes are accepted by knative.dev/sample-controller

```yaml
steps:
  - name: Set up Go 1.15.x
    uses: actions/setup-go@v2
    with:
      go-version: 1.15.x
  - name: Checkout Upstream
    uses: actions/checkout@v2
    with:
      path: ./src/knative.dev/pkg
  - name: Checkout Downstream
    uses: actions/checkout@v2
    with:
      repository: knative-sandbox/sample-controller
      path: ./src/knative.dev/sample-controller
  - uses: knative-sandbox/actions-downstream-test@v1
    with:
      upstream-module: knative.dev/pkg
      downstream-module: knative.dev/sample-controller
```
