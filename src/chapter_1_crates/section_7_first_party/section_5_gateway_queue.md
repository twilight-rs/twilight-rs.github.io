# Gateway queue

`twilight-gateway-queue` is a set of a set of a trait and a few implementations
of it that is used by the [gateway] to ratelimit `identify` calls. It will most
of the time not be used directly, but instead through the reexport from the 
[gateway].

## Installation

Add the following yo your `Cargo.toml`:
```toml
twilight-gateway-queue = "0.1.0"
```

## Links

*source*: <https://github.com/twilight-rs/twilight/tree/trunk/gateway/queue>

*docs*: <https://api.twilight.rs/twilight_gateway_queue/index.html>

*crates.io*: <https://crates.io/crates/twilight-gateway-queue>

[gateway]: ../section_3_gateway.html
