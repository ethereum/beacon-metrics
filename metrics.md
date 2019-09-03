# Beacon chain metrics

## Introduction

This specification encodes the behavior of sampling and collection of metrics by beacon chain clients.

This specification is informative, and implementations are not required to implement all recommendations.

## Metrics collection

Beacon chain clients SHOULD use Prometheus for metrics collection conforming to the following:

* Beacon chain clients SHOULD configure [Prometheus](https://prometheus.io/) so that it exposes metrics collection over an HTTP port.
* Beacon chain clients MAY elect to secure the HTTP endpoint by restricting network access and applying Prometheus security settings, according to Prometheus [best practices](https://prometheus.io/docs/operating/security/).
* Beacon chain clients SHOULD allow configuration flags to set the network interface and the port the Prometheus collection endpoint will be served from.
* By default, the Prometheus collection endpoint SHOULD be served from 0.0.0.0:8008.

## Metrics

This section defines a set of metrics to be sampled by beacon chain clients.

### Rationale

The metrics SHOULD behave under the guidelines set by the [Prometheus documentation](https://prometheus.io/docs/practices/instrumentation/#things-to-watch-out-for).

### Interop Metrics

The following are the minimal metrics agreed to be conformed upon prior to initial client interop efforts.

| Name | Metric type | Usage | Sample collection event |
|-----------------------------------------------|-------------|------------------------------------------------------------------------|----------------------|
| `beaconchain_peers`                           | Gauge       | Tracks number of peers                                                 | On peer add/drop     |
| `beaconchain_slot`                            | Gauge       | Latest slot of the beacon chain state                                  | On slot              |
| `beaconchain_head_slot`                       | Gauge       | Slot of the head block of the beacon chain                             | On fork choice       |
| `beaconchain_head_root`                       | Gauge       | Root of the head block of the beacon chain                             | On fork choice       |
| `beaconchain_finalized_epoch`                 | Gauge       | Current finalized checkpoint epoch                                     | On epoch transition  |
| `beaconchain_finalized_root`                  | Gauge       | Current finalized checkpoint root                                      | On epoch transition  |
| `beaconchain_current_justified_epoch`         | Gauge       | Current justified checkpoint epoch                                     | On epoch transition  |
| `beaconchain_current_justified_root`          | Gauge       | Current justified checkpoint root                                      | On epoch transition  |
| `beaconchain_previous_justified_epoch`        | Gauge       | Current previously justified checkpoint epoch                          | On epoch transition  |
| `beaconchain_previous_justified_root`         | Gauge       | Current previously justified checkpoint root                           | On epoch transition  |

### Additional Metrics

The following are proposed metrics to be added to clients. This list is _not_ stable and is subject to drastic changes, deletions, and additions.

| Name | Metric type | Usage | Sample collection event |
|-----------------------------------------------|-------------|--------------------------------------------------------------------------------------|---------------------|
| `beaconchain_current_validators`              | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in current epoch  | On epoch transition |
| `beaconchain_previous_validators`             | Gauge       | Number of `status="pending\|active\|exited\|withdrawable"` validators in previous epoch | On epoch transition |
| `beaconchain_current_live_validators`         | Gauge       | Number of active validators that successfully included attestation on chain for current epoch     | On block  |
| `beaconchain_previous_live_validators`        | Gauge       | Number of active validators that successfully included attestation on chain for previous epoch    | On block  |
| `beaconchain_pending_deposits`                | Gauge       | Number of pending deposits (`state.eth1_data.deposit_count - state.eth1_deposit_index`)           | On block  |
| `beaconchain_processed_deposits_total`        | Gauge       | Number of total deposits included on chain                                                        | On block  |
| `beaconchain_pending_exits`                   | Gauge       | Number of pending voluntary exits in local operation pool                                         | On slot   |
| `beaconchain_previous_epoch_orphaned_blocks`  | Gauge       | Number of blocks orphaned in the previous epoch                                         | On epoch transition |
| `beaconchain_reorgs_total`                    | Counter     | Total occurrences of reorganizations of the chain                                            | On fork choice |

### Labels

The metrics should be collected without labels unless specified. The collection process might add additional labels as metadata regarding the machine and build information.
