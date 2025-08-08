# Mainnet Consensus Layer Metrics

## Introduction

This specification encodes the behavior of sampling and collection of metrics by execution layer clients on mainnet.

This specification is informative, and implementations are not required to implement all recommendations.

## Metrics

This section defines a set of metrics to be sampled by beacon chain clients.

### Rationale

The metrics SHOULD behave under the guidelines set by the [Prometheus documentation](https://prometheus.io/docs/practices/instrumentation/#things-to-watch-out-for).

### Labels

The metrics should be collected without labels unless specified. The collection process might add additional labels as metadata regarding the machine and build information.

## Prometheus metrics collection

A beacon chain client using Prometheus for metrics collection SHOULD conform to the following:

* Beacon chain clients SHOULD configure [Prometheus](https://prometheus.io/) so that it exposes metrics collection over an HTTP port.
* Beacon chain clients MAY elect to secure the HTTP endpoint by restricting network access and applying Prometheus security settings, according to Prometheus [best practices](https://prometheus.io/docs/operating/security/).
* Beacon chain clients SHOULD allow configuration flags to set the network interface and the port the Prometheus collection endpoint will be served from.
* By default, the Prometheus collection endpoint SHOULD be served from 0.0.0.0:8008.
