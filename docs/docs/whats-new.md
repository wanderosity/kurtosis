---
title: What's New In Kurtosis
sidebar_label: What's New
slug: '/whats-new'
toc_max_heading_level: 2
---

# What's New In Kurtosis

For detailed information about the changes in each release, see [the changelog](/changelog).

## 2025-05-05

### Logging Architecture Improvements

Kurtosis now supports exporting logs from enclaves to external systems like Elasticsearch, CloudWatch, S3, and more. Built on top of [Vector](https://vector.dev/), this new logging architecture enables highly flexible log forwarding via configurable "sinks" in your Kurtosis config file.

This unlocks new capabilities, including:

- Streaming logs to observability platforms like Kibana, OpenSearch, or Loki
- Long-term log storage in cloud services like AWS S3
- Integration with security and audit pipelines
- Real-time search and filtering of logs
- Custom filtering and transformation using Fluent Bit-style filters

You can configure different sinks per cluster, and supported sink types mirror those provided by Vector.

To get started, check out our guide on [Exporting Logs to External Services](./guides/exporting-logs.md).

### `service update` Command

A new `service update` command lets you modify services in-place within a running enclave—without tearing down the entire environment.

Use it to update only the parts of the service config you want, including:

- `--image` – update the container image
- `--entrypoint` – override the binary the container runs
- `--env` – add or override environment variables
- `--ports` – change private port definitions
- `--files` – mount new or updated file artifacts
- `--cmd` – override the command executed in the container

Example:

```bash
kurtosis service update my-enclave test-service \
  --image my-custom-image \
```


2024-02-26
----------

### Enclave Builder UI

You can now build enclaves without writing code using the enclave builder UI:

![enclave-builder.png](../static/img/whats-new/2024-02-26/enclave-builder.png)

The UI will automatically generate Starlark for you, which can be viewed with the "Preview" button.

To enable the enclave builder UI, go to the "About" icon in the bottom-left corner of the Kurtosis app and select "Enable experimental enclave builder interface". You'll then see an "Enclave Builder" button in the Enclave List screen.

### Kurtosis Github Action

You can now run Kurtosis inside your GH Actions CI using [our prebuilt Action](https://github.com/kurtosis-tech/kurtosis-github-action).

```yaml
- name: Kurtosis Tests
  uses: kurtosis-tech/kurtosis-github-action@v1
  with:
    path: 'github.com/my-org/my-kurtosis-package'  # Can also be the path to a 
                                                   # Kurtosis package in the repo
                                                   # For example:
                                                   # './path/to/kurtosis-package'
    args: './test-args.yaml'
```

This can be useful for integration & end-to-end tests, and can be paired with [ImageBuildSpec](https://docs.kurtosis.com/api-reference/starlark-reference/image-build-spec/) so that Kurtosis will both build the image and instantiate the environment.

### Human-friendly plan steps

The default way `kurtosis run` describes plan steps is now human-friendly:

![human-friendly-descriptions.png](../static/img/whats-new/2024-02-26/human-friendly-descriptions.png)

You can return to the previous way by adding `--verbosity brief` to your `kurtosis run` flags.

### Bugs & Feedback

You can now submit bugs from the Kurtosis app itself using the button in the bottom-left:

![bug-reports.png](../static/img/whats-new/2024-02-26/bug-reports.png)

We're very interested in your feedback about the above features, so let us know what you think!
