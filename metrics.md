# Beacon chain metrics

## Introduction

This specification encodes the behavior of sampling and collection of metrics by beacon chain clients.
This specification is informative, and implementations are not required to implement all recommendations.

## Metrics collection

Beacon chain clients should use Prometheus for metrics collection.

Beacon chain clients should configure [Prometheus](https://prometheus.io/) so that it exposes metrics collection over a HTTP port.
Beacon chain clients may elect to secure the HTTP endpoint by restricting network access and applying Prometheus security settings, according to Prometheus [best practices](https://prometheus.io/docs/operating/security/).
Beacon chain clients should allow configuration flags to set the network interface and the port the Prometheus collection endpoint will be served from.
By default, the Prometheus collection endpoint should be served from 0.0.0.0:8008.

## Metrics

This section defines a set of metrics to be sampled by beacon chain clients.

### Rationale

The metrics should behave under the guidelines set by the [Prometheus documentation](https://prometheus.io/docs/practices/instrumentation/#things-to-watch-out-for).

### Metrics

| Name | Metric type | Usage | Sample collection event |
|---------------------------------|-------------|-------------------------------------------------------------------|-------------------------------------|
| beaconchain_peers              | Gauge       | Tracks number of peers                                            | When a new peer is added or dropped |
| beaconchain_current_slot | Gauge | Latest slot recorded by the beacon chain | Each time slot changes |
| beaconchain_current_justified_epoch         | Gauge       | Current justified epoch                                           | On each epoch                       |
| beaconchain_current_finalized_epoch         | Gauge       | Current finalized epoch                                           | On each epoch                       |
| beaconchain_current_prev_justified_epoch    | Gauge       | Current previously justified epoch                                | On each epoch                       | 
| beaconchain_current_epoch_live_validators   | Gauge       | Number of active validators who reported for the current epoch    | On each epoch                       |
| beaconchain_previous_epoch_live_validators  | Gauge       | Number of active validators who reported for the previous epoch   | On each epoch
| beaconchain_reorg_events_total              | Counter     | Occurrence of a reorganization of the chain                       | On fork choice                      |
| beaconchain_pending_deposits                | Gauge       | Number of pending deposits                                        | Upon processing eth1 events watching the deposit contract |
| beaconchain_total_deposits                  | Gauge       | Number of total deposits                                          | Upon processing eth1 events watching the deposit contract |


### Labels

The metrics should be collected without labels at all if possible. The collection process will add additional labels as metadata regarding the machine and build information.
