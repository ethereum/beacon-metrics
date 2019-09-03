# Beacon chain metrics

## Introduction

This specification encodes the behavior of sampling and collection of metrics by beacon chain clients.

This specification is informative, and implementations are not required to implement all recommendations.

## Metrics

This section defines a set of metrics to be sampled by beacon chain clients.

### Rationale

The metrics SHOULD behave under the guidelines set by the [Prometheus documentation](https://prometheus.io/docs/practices/instrumentation/#things-to-watch-out-for).

### Interop Metrics

The following are the minimal metrics agreed to be conformed upon prior to initial client interop efforts.

| Name | Metric type | Usage | Sample collection event |
|------------------------------------------|-------------|-------------------------------------------------------------|----------------------|
| `libp2p_peers`                           | Gauge       | Tracks number of libp2p peers                               | On peer add/drop     |
| `beacon_slot`                            | Gauge       | Latest slot of the beacon chain state                       | On slot              |
| `beacon_head_slot`                       | Gauge       | Slot of the head block of the beacon chain                  | On fork choice       |
| `beacon_head_root`                       | Gauge       | Root of the head block of the beacon chain                  | On fork choice       |
| `beacon_finalized_epoch`                 | Gauge       | Current finalized epoch                                     | On epoch transition  |
| `beacon_finalized_root`                  | Gauge       | Current finalized root                                      | On epoch transition  |
| `beacon_current_justified_epoch`         | Gauge       | Current justified epoch                                     | On epoch transition  |
| `beacon_current_justified_root`          | Gauge       | Current justified root                                      | On epoch transition  |
| `beacon_previous_justified_epoch`        | Gauge       | Current previously justified epoch                          | On epoch transition  |
| `beacon_previous_justified_root`         | Gauge       | Current previously justified root                           | On epoch transition  |

### Additional Metrics

The following are proposed metrics to be added to clients. This list is _not_ stable and is subject to drastic changes, deletions, and additions.

| Name | Metric type | Usage | Sample collection event |
|------------------------------------------|-------------|--------------------------------------------------------------------------------------|---------------------|
| `beacon_current_validators`              | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in current epoch  | On epoch transition |
| `beacon_previous_validators`             | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in previous epoch | On epoch transition |
| `beacon_current_live_validators`         | Gauge       | Number of active validators that successfully included attestation on chain for current epoch     | On block  |
| `beacon_previous_live_validators`        | Gauge       | Number of active validators that successfully included attestation on chain for previous epoch    | On block  |
| `beacon_pending_deposits`                | Gauge       | Number of pending deposits (`state.eth1_data.deposit_count - state.eth1_deposit_index`)           | On block  |
| `beacon_processed_deposits_total`        | Gauge       | Number of total deposits included on chain                                                        | On block  |
| `beacon_pending_exits`                   | Gauge       | Number of pending voluntary exits in local operation pool                                         | On slot   |
| `beacon_previous_epoch_orphaned_blocks`  | Gauge       | Number of blocks orphaned in the previous epoch                                         | On epoch transition |
| `beacon_reorgs_total`                    | Counter     | Total occurrences of reorganizations of the chain                                            | On fork choice |

### Labels

The metrics should be collected without labels unless specified. The collection process might add additional labels as metadata regarding the machine and build information.

## Prometheus metrics collection

A beacon chain client using Prometheus for metrics collection SHOULD conform to the following:

* Beacon chain clients SHOULD configure [Prometheus](https://prometheus.io/) so that it exposes metrics collection over an HTTP port.
* Beacon chain clients MAY elect to secure the HTTP endpoint by restricting network access and applying Prometheus security settings, according to Prometheus [best practices](https://prometheus.io/docs/operating/security/).
* Beacon chain clients SHOULD allow configuration flags to set the network interface and the port the Prometheus collection endpoint will be served from.
* By default, the Prometheus collection endpoint SHOULD be served from 0.0.0.0:8008.
